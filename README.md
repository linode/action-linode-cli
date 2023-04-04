# GitHub Action for Linode CLI

This GitHub Action allows users to quickly install and authenticate the Linode CLI in a GitHub Actions workflow.

See the [official Linode CLI repository](https://github.com/linode/linode-cli) for specific usage instructions.

## Arguments

This GitHub Action exposes the following arguments:

| Name      | Required | Default | Description                                                                                                                                |
|-----------|----------|---------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `token`   | No       | None    | The [Linode Personal Access Token](https://www.linode.com/docs/products/tools/api/guides/manage-api-tokens/) to authenticate the CLI with. |
| `version` | No       | latest  | The version of the Linode CLI to install.                                                                                                  |

## Getting Started

Before starting, you must create a [Linode Personal Access Token](https://www.linode.com/docs/products/tools/api/guides/manage-api-tokens/) to authenticate the Linode CLI with.

In order to install and authenticate the Linode CLI within a GitHub Action workflow, 
add the following workflow step:

```yaml
- name: Install the Linode CLI
  uses: linode/action-linode-cli@v1
  with:
    token: ${{ secrets.LINODE_TOKEN }}
```

The Linode CLI should now be available in your GitHub Actions shell environment:

```yaml
- name: List Linodes
  run: linode-cli linodes ls --json
```

### Using a Specific CLI Version

In order to use a specific version of the Linode CLI, you can use the `version` argument:

```yaml
- name: Install the Linode CLI
  uses: linode/action-linode-cli@v1
  with:
    token: ${{ secrets.LINODE_TOKEN }}
    version: 5.35.0
```

**NOTE: Certain older Linode CLI versions may not be compatible with this GitHub action.**

### Skipping Authentication

In order to skip the authentication during setup, you can exclude the `token` argument:

```yaml
- name: Install the Linode CLI
  uses: linode/action-linode-cli@v1
```

You can then authenticate the Linode CLI at runtime using the `LINODE_CLI_TOKEN` environment variable:

```yaml
- name: List Linodes
  run: linode-cli linodes ls --json
  env:
    LINODE_CLI_TOKEN: ${{ secrets.LINODE_TOKEN }}
```


## Contribution Guidelines

Want to improve **action-linode-cli**? Please start [here](CONTRIBUTING.md).

## License

This project is released under the [Apache-2.0 license](./LICENSE).