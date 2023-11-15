# action-tfswitch

A github action to run [tfswitch](https://tfswitch.warrensbox.com/) as a [composite action](https://github.com/orgs/community/discussions/36861)

## Why

The official hashicorp [setup-terraform](https://github.com/hashicorp/setup-terraform) provides the same ability to configure the version, with a key difference that the version _needs_ to be specified in the pipeline file. For cases where tfswitch is used in the development process, and the version is already defined, and checked in, in:

- `.terraform-version`
- `versions.tf`

.. or any other way [supported by tfswitch](https://tfswitch.warrensbox.com/Quick-Start/), this provides for a seamless experience working locally, or in Github Actions.

## Usage

To use tfswitch github action, configure a YAML workflow file, e.g.

### Using the required_version block

Recommended - <https://developer.hashicorp.com/terraform/language/settings#specifying-a-required-terraform-version>

Contents of `versions.tf`

```hcl
terraform {
  ...
  required_version = "1.6.3"
  ...
}
```

Workflow

```yaml
jobs:
  tfswitch-version-from-required_version:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Setup tfswitch
      uses: stv-io/action-tfswitch@v1
    - name: Install
      run: |
        tfswitch
        terraform --version
        ...
```

### Using environment variables

```yaml
jobs:
  tfswitch-version-as-env-var:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Setup tfswitch
      uses: stv-io/action-tfswitch@v1
    - name: Install
      env:
        TF_VERSION: 1.6.2
      run: |
        tfswitch
        terraform --version
        ...
```

### Specify version on the command line

```yaml
jobs:
  tfswitch-version-as-parameter:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Setup tfswitch
      uses: stv-io/action-tfswitch@v1
    - name: Install
      run: |
        tfswitch 1.6.4
        terraform --version
        ...
```

## Note

This action unlinks the default installed terraform which is available in the [runner](https://github.com/actions/runner-images/tree/main).

## Credit

<https://github.com/warrensbox/terraform-switcher>
