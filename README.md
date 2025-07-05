# pgrubic-action

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
[![CI](https://github.com/bolajiwahab/pgrubic-action/actions/workflows/ci.yml/badge.svg)](https://github.com/bolajiwahab/pgrubic-action/actions/workflows/ci.yml)

A GitHub Action to run [**pgrubic**](https://bolajiwahab.github.io/pgrubic), a PostgreSQL linter and formatter for schema migrations and design best practices.

This action runs `pgrubic lint` by default, but it can do
anything `pgrubic` can.

## Inputs

| Input             | Description                                                                                                            | Default            |
|-------------------|------------------------------------------------------------------------------------------------------------------------|--------------------|
| `args`            | The arguments to pass to the **pgrubic** command. See [Running pgrubic](https://bolajiwahab.github.io/pgrubic/cli/).   | `lint`             |
| `pgrubic-version` | The version of **pgrubic** to use, e.g., `0.6.0`.                                                                      | `latest`           |
| `src`             | The directory or files to run **pgrubic** on.                                                                          | [github.workspace](https://docs.github.com/en/actions/reference/contexts-reference#github-context:~:text=the%20workflow%20file.-,github.workspace,-string)                                                   |

## Outputs

| Output                      | Description                                 |
|-----------------------------|---------------------------------------------|
| `installed-pgrubic-version` | The version of the installed **pgrubic**.   |

## Usage

### Basic

```yaml
- uses: bolajiwahab/pgrubic-action@v1
```

### Specifying a different source directory

```yaml
- uses: bolajiwahab/pgrubic-action@v1
  with:
    src: "./src"
```

### Specifying multiple files

```yaml
- uses: bolajiwahab/pgrubic-action@v1
  with:
    src: >-
      path/to/file1.sql
      path/to/file2.sql
```

### Specifying multiple directories

```yaml
- uses: bolajiwahab/pgrubic-action@v1
  with:
    src: >-
      path/to/dir1
      path/to/dir2
```

### Specifying multiple files and directories

```yaml
- uses: bolajiwahab/pgrubic-action@v1
  with:
    src: >-
      path/to/file1.sql
      path/to/file2.sql
      path/to/dir1
      path/to/dir2
```

### To install pgrubic

This action adds **pgrubic** to the PATH, so you can use it in subsequent steps.

```yaml
- uses: bolajiwahab/pgrubic-action@v1
- run: pgrubic lint
- run: pgrubic format
```

By default, this action runs `pgrubic lint` after installation. If you do not want to run any `pgrubic` command but only install it,
you can use the `args` input to overwrite the default option (`lint`):

```yaml
- name: Install pgrubic without running lint or format
  uses: bolajiwahab/pgrubic-action@v1
  with:
    args: "--version"
```

### Use `pgrubic format`

```yaml
- uses: bolajiwahab/pgrubic-action@v1
  with:
    args: "format --check --diff"
```

### Install a specific version of pgrubic

```yaml
- uses: bolajiwahab/pgrubic-action@v1
  with:
    pgrubic-version: "0.6.0"
```

### Install the latest version of pgrubic

```yaml
- uses: bolajiwahab/pgrubic-action@v1
  with:
    pgrubic-version: "latest"
```

## Contributing

We welcome and greatly appreciate contributions. If you would like to contribute, please see the [contributing guidelines](contributing.md).

## Support

Encountering issues? Take a look at the existing GitHub [issues](https://github.com/bolajiwahab/pgrubic-action/issues), and don't hesitate to open a new one.

## License

MIT license.
