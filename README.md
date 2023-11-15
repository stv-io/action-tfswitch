# action-tfswitch

A github action to run [tfswitch](https://tfswitch.warrensbox.com/) as a [composite action](https://github.com/orgs/community/discussions/36861)

## Usage

To use tfswitch github action, configure a YAML workflow file, e.g.
`.github/workflows/tfswitch.yml`, with the following:

```yaml
name: Install terraform via tfswitch

on:
  - pull_request

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Setup tfswitch
      uses: stv-io/action-tfswitch@main
    - name: Install
      run: |
        tfswitch 1.6.4
        terraform --version
        terraform init
        ...
```

## Credit

<https://github.com/warrensbox/terraform-switcher>
