# `release version find`

Находит релизную версию по заданным критериям.

По умолчанию находит последнюю релизную версию.

Может сформировать версию для следующего релиза или найти версию в названии релизной ветки.

## Usage

```console
$ npx release version find -h

release version find

Search release versions.

Version:
  --latest       Returns last version of release                       [boolean]
  --next         Returns next version of future release
           [string] [choices: "major", "premajor", "minor", "preminor", "patch",
                                                       "prepatch", "prerelease"]
  --from-branch  Parse release version from specified branch            [string]
  --from-issue   Parse release version from issue                       [string]

Options:
  --config
  --help, -h  Show help                                                [boolean]

Git Repository:
  --git                Git parameters                              [default: {}]
  --git.repository     Git url to repository                            [string]
  --git.baseBranch     Base branch of repository                        [string]
  --git.releaseBranch  Pattern of release branch. Use a placeholder {{version}}
                       in this pattern, e.g. "release/v{{version}}"     [string]
  --git.releaseTag     Pattern of release tag. Use a placeholder {{version}} in
                       this pattern, e.g. "v{{version}}"                [string]

Issue search parameters:
  --issue              Startrek issue parameters
  --issue.<parameter>  Startrek filters for find query, e.g. author, tags and
                       other filters
  --issue.resolution                               [string] [default: "empty()"]
  --issue.queue                                                         [string]
  --issue.searchQuery  Startrek query overrides parameters precified in "issue".
                       Query language docs: https://nda.ya.ru/3SdFPJ    [string]

Placeholders:
  --placeholders  Placeholders for configuration values {{key}}: key=value
                                                                         [array]

Examples:
  $ release version find --latest
  $ release version find --next --hotfix
  $ release version find --branch="release/ydo/v1.2.3"

Config:
  Git parameters can be specified in release config "git" section.

  "git": {
      "repository": "git@github.yandex-team.ru:owner/repo.git",
      "baseBranch": "master",
      "releaseBranch": "release/v{{version}}",
      "releaseTag": "v{{version}}"
  }

  Parameters can be passed as command arguments, e.g:

  $ release version find --git.repository
  git@github.yandex-team.ru:owner/repo.git
    \ --git.baseBranch master
    \ --git.releaseBranch "release/v{{version}}"
    \ --git.releaseTag "v{{version}}"

  You can use {{placeholders}} in parameters. Their values must be specified via
  --placeholders option.

  $ release version find --config ./path/to/config --placeholders
  branch-prefix=release service=my-service

  "git": {
      "repository": "git@github.yandex-team.ru:owner/repo.git",
      "baseBranch": "master",
      "releaseBranch": "{{branch-prefix}}/{{service}}/v{{version}}",
      "releaseTag": "{{service}}/v{{version}}"
  }
```
