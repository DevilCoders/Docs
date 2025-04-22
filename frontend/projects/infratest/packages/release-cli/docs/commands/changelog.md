# `release changelog`

Строит changelog.

По умолчанию возвращает изменения, сделанные после последнего релиза.

## Usage

```console
$ npx release changelog -h

release changelog

Build changelog

Changelog:
  --from                                Release version from which need to build
                                        changelog. Specify "latest" to build
                                        changelog from latest release version.
                                                    [string] [default: "latest"]
  --to                                  Release version to which need to build
                                        changelog. Specify "next" to build
                                        changelog with changes that are not
                                        included in last release.
                                                      [string] [default: "next"]
  --changelog                           Changelog parameters       [default: {}]
  --changelog.issues.components.only    Leave only issues with specified
                                        components.                      [array]
  --changelog.issues.components.ignore  Leave only issues without specified
                                        components.                      [array]

Options:
  --config
  --help, -h  Show help                                                [boolean]

Issue search parameters:
  --issue              Startrek issue parameters
  --issue.<parameter>  Startrek filters for find query, e.g. author, tags and
                       other filters
  --issue.resolution                               [string] [default: "empty()"]
  --issue.queue                                                         [string]
  --issue.searchQuery  Startrek query overrides parameters precified in "issue".
                       Query language docs: https://nda.ya.ru/3SdFPJ    [string]

Project:
  --project       Project parameters                               [default: {}]
  --project.path  Relative path from root of repository to directory with
                  project sources                                       [string]

Placeholders:
  --placeholders  Placeholders for configuration values {{key}}: key=value
                                                                         [array]

Examples:
  $ release changelog --from=latest
  $ release changelog --from=v1.2.3 --to=v2.0.0
  $ release changelog --branch="release/ydo/v1.2.3"

Config:
  Git and project parameters can be specified in release config.

  {
    "git": {
      "repository": "git@github.yandex-team.ru:owner/repo.git",
      "baseBranch": "master"
    },
    "project": {
      "path": "services/my-service"
    }
  }

  Parameters can be passed as command arguments, e.g:

  $ release version --git.repository git@github.yandex-team.ru:owner/repo.git
    \ --git.baseBranch master
    \ --project.path services/my-service

  You can use {{placeholders}} in parameters. Their values must be specified via
  --placeholders option.

  $ release version --config ./path/to/config --placeholders owner=my-owner
  project=my-project

  {
    "git": {
      "repository": "git@github.yandex-team.ru:{{owner}}/{{project}}.git",
      "baseBranch": "master",
    },
    "project": {
      "path": "services/{{project}}"
    }
  }
```