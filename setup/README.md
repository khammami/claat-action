# CLaaT (Codelabs as a Thing) Setup

This composite action install [CLaaT](https://github.com/googlecodelabs/tools) ((as a go module, go setup is included v1.18)

To install `claat` on your machine:

```bash
go install github.com/googlecodelabs/tools/claat@latest`
```

To check available [commands and flags](docs/claat_command_help.md) of `claat`:

```bash
claat help
```

## Inputs

| **Input**     | **Description**                               | **Required** |
|---------------|-----------------------------------------------|--------------|
| `version`     | CLaaT version <br> Default (action): `latest` | No           |

## Example Usage

```yaml
name: Workflow Sample

on:
  push:

jobs:
  export:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4

    - name: Setup claat
      uses: "khammami/claat-action/setup@[version|main]"

```

## License

The scripts and documentation in this project are released under the [Apache 2.0 License](LICENSE)

## Code of Conduct

:wave: Be nice. See [our code of conduct](.github/CODE_OF_CONDUCT.md)
