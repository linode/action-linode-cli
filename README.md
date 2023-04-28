# GitHub Action for Linode CLI

This GitHub Action allows users to quickly install and authenticate the Linode CLI in a GitHub Actions workflow.

See the [official Linode CLI repository](https://github.com/linode/linode-cli) for specific usage instructions.

This GitHub Action is designed to run on Ubuntu-based runners and may not function as intended on other platforms.  

## Arguments

This GitHub Action exposes the following arguments:

| Name           | Required | Default | Description                                                                                                                                                                       |
|----------------|----------|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `token`        | No       | None    | The [Linode Personal Access Token](https://www.linode.com/docs/products/tools/api/guides/manage-api-tokens/) to authenticate the CLI with.                                        |
| `version`      | No       | latest  | The version of the Linode CLI to install.                                                                                                                                         |
| `setup-python` | No       | true    | If true, Python will automatically be installed on the runner. If false, users are expected to have a functioning Python installation on their runner before running this action. | 

## Getting Started

Before starting, you must create a [Linode Personal Access Token](https://www.linode.com/docs/products/tools/api/guides/manage-api-tokens/) to authenticate the Linode CLI with.

Linode Personal Access Tokens should be stored as [Encrypted Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) to ensure they are secure and sanitized from workflow outputs. 

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

This software is provided by Linode, a wholly owned subsidiary of Akamai Technologies Inc. (“Akamai”).  This software may collect or transmit personal or sensitive information provided by or obtained from End Users, subject to the policies and terms of use of Akamai.  [This statement](https://www.akamai.com/legal/privacy-and-policies/privacy-statement) describes in detail how Akamai collects, uses, and shares information about individuals who interact with Akamai via its websites, online portals, mobile applications, or directly with Akamai employees and representatives, as well as by using the services of Akamai customers.

The software and documentation in this project are released under the [BSD-3-Clause license](./LICENSE).