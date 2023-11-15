# action-tfswitch

A github action to run tfswitch as a composite action

## Usage

To use tfswtich github action, configure a YAML workflow file, e.g.
`.github/workflows/tfswitch.yml`, with the following:

```yaml
name: Run terraform
on:
  - pull_request
jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4

    - name: Render terraform docs inside the README.md and push changes back to PR branch
      uses: stv-io/action-tfswitch@main
    - name: Render terraform docs inside the README.md and push changes back to PR branch
      run: |
        export TF_VERSION=1.6.1
        tfswitch 1.6.2
        terraform --version
```
