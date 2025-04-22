# testpalm-cli

> CLI-утилита для работы с TestPalm.

## Установка

```shell
npm install @yandex-int/si.ci.testpalm-cli --registry=https://npm.yandex-team.ru
```

## Команды

### clone

```console
testpalm.js clone <source> <target>

Clone source project to target with another id.

Requires TestPalm API token in TESTPALM_OAUTH_TOKEN environment variable.

Options:
  --help, -h                      Show help                            [boolean]
  --version, -v                   Show version number                  [boolean]
  --title                         Set the specified title to created project
                                                                        [string]
  --copy-cases                    Copy test cases from source project to created
                                  project              [boolean] [default: true]
  --copy-runs                     Copy test runs from source project to created
                                  project             [boolean] [default: false]
  --copy-versions                 Copy versions from source project to created
                                  project             [boolean] [default: false]
  --suppress-exist-project-error  Don't throw an error when target project is
                                  already exist       [boolean] [default: false]
  --silent                        Don't flush messages to stdout or stderr
                                                      [boolean] [default: false]
  --json                          Flush response body to stdout (project can
                                  contain tokens)     [boolean] [default: false]
```

### fetch-test-cases

```console
testpalm fetch-test-cases <project>

Fetch test cases from project.

Requires TestPalm API token in TESTPALM_OAUTH_TOKEN environment variable.

Options:
  --help, -h           Show help                                       [boolean]
  --version, -v        Show version number                             [boolean]
  --project            TestPalm project                                 [string]
  --include            List of fields to get for test cases. By default, all
                       fields are returned                 [array] [default: []]
  --apply-definitions  Apply definitions to test case attributes[default: false]
```
