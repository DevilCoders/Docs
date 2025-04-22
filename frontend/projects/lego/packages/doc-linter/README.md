# doc-linter

* [Install](#install)
* [Using CLI](#using-cli)


## Install

```
npm install @yandex-lego/doc-linter --save
```

## Using CLI

* `doc-linter --version` — Print doc-linter version.
* `doc-linter --help` — Display help for the command.
* `doc-linter --init` — Save default config ".doclinterrc" in current directory
* `doc-linter` — Start listing all default blocks.
* `doc-linter -b [value]` — Block of the islands to lint, for example `doc-linter -b select2`.
* `doc-linter -i [value]` — Block of the islands to ignore, for example `doc-linter -i select2`.
* `doc-linter -i` — Blocks of the islands to ignore, определенные в файле `.doclinterignore.json`.


