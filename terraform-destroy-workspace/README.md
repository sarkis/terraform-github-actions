# terraform-destroy-workspace action

This is one of a suite of terraform related actions - find them at [dflook/terraform-github-actions](https://github.com/dflook/terraform-github-actions).

This action uses the `terraform destroy` command to destroy all resources in a terraform workspace and then delete the workspace.

## Inputs

* `path`

  Path to the terraform configuration

  - Type: string
  - Required

* `workspace`

  Terraform workspace to destroy and delete

  - Type: string
  - Required

* `var`

  Comma separated list of terraform vars to set

  - Type: string
  - Optional

* `var_file`

  Comma separated list of terraform var files

  - Type: string
  - Optional

* `backend_config`

  Comma separated list of terraform backend config values.

  - Type: string
  - Optional

* `backend_config_file`

  Comma separated list of terraform backend config files.

  - Type: string
  - Optional

* `parallelism`

  Limit the number of concurrent operations

  - Type: number
  - Optional
  - Default: 10

## Example usage

This example deletes the workspace named after the git branch when the associated PR is closed.

```yaml
name: Cleanup

on:
  pull_request:
    types: [closed] 

jobs:
  check_format:
    runs-on: ubuntu-latest
    name: Destroy workspace
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: terraform destroy
        uses: ./terraform-destroy-workspace
        with:
          path: my-terraform-config
          workspace: ${{ github.head_ref }}
```