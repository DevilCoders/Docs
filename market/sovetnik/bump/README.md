# bump

`bump` updates package version.

## Overview

`bump` does the following:

- updates version in `package.json`
- updates version in `package-lock.json` (if exists)
- updates version in *debian package* files:
  - *control* file
  - *changelog* file
- creates `CHANGELOG.md` in project root
- creates an annotated *git tag*
- commits and pushes changes to the *remote*

## How to install

1. go to [releases page](https://github.yandex-team.ru/vkozelsky/bump/releases)
2. run command from the particular release in your Terminal

Or you can do all steps manually:

1. download the binary
2. untar it: `tar -xzvf bump.tar.gz`
3. and put to *bin* folder: `cp bump /usr/local/bin`

Check your installation in Terminal by typing the following:

```sh
bump -h
```

## Usage

```console
USAGE:
    bump <version_type>

ARGS:
    <version_type>    [possible values: major, minor, patch]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information
```
