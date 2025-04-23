# `release close`

Закрывает указанный релиз.

По умолчанию закрывает все открытые релизы.

## Usage

```console
$ npx release close -h

release close

Close release issue

Release:
  --version     Version numbers (semver) of releases that should be closed
                                                                        [string]
  --resolution  Resolution for release issue close state
                                                   [string] [default: "invalid"]
  --create-tag  Create release tag on HEAD commit of release branch    [boolean]

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

Git Repository:
  --git                Git parameters                              [default: {}]
  --git.repository     Git url to repository                            [string]
  --git.baseBranch     Base branch of repository                        [string]
  --git.releaseBranch  Pattern of release branch. Use a placeholder {{version}}
                       in this pattern, e.g. "release/v{{version}}"     [string]
  --git.releaseTag     Pattern of release tag. Use a placeholder {{version}} in
                       this pattern, e.g. "v{{version}}"                [string]

Placeholders:
  --placeholders  Placeholders for configuration values {{key}}: key=value
                                                                         [array]


Close release issue and optionally removes it's artifacts.

By default, all issues are found dy filters specified in "issue" config section,
then the corresponding git release branches are closed.

The release of a specific version can be closed by specifying the --version
parameter.

Configuration:
  {
    "issue": {
        "queue": "SEAREL",
        "tags": "report-templates",
        "summary": "si/frontend@ydo/{{version}}"
    },
    "git": {
        "repository": "git@github.yandex-team.ru:juliethefox/frontend.git",
        "baseBranch": "master",
        "releaseBranch": "release/health/v{{version}}",
        "releaseTag": "ydo/v{{version}}"
    },
    "command": {
        "close": {
            "removeBranch": true,
            "createTag": false
        }
    }
```
