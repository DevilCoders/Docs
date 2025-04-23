# `release create`

Создаёт новый релиз.

В зависимости от конфигурации может:

1. Запускать проверки перед созданием релиза.
1. Отводить релизную ветку.
1. Создавать релизную задачу.

## Usage

```console
$ npx release create -h

release create

Create release

Release:
  --version        Version for new release. You can specify semantic release
                   type.                                     [string] [required]
  --check          Check ability to create release                     [boolean]
  --create-issue   Create release issue                                [boolean]
  --create-branch  Create release branch                               [boolean]

Git Repository:
  --git                Git parameters                              [default: {}]
  --git.repository     Git url to repository                            [string]
  --git.baseBranch     Base branch of repository                        [string]
  --git.releaseBranch  Pattern of release branch. Use a placeholder {{version}}
                       in this pattern, e.g. "release/v{{version}}"     [string]
  --git.releaseTag     Pattern of release tag. Use a placeholder {{version}} in
                       this pattern, e.g. "v{{version}}"                [string]

Project:
  --project       Project parameters                               [default: {}]
  --project.path  Relative path from root of repository to directory with
                  project sources                                       [string]

Issue search parameters:
  --issue              Startrek issue parameters
  --issue.<parameter>  Startrek filters for find query, e.g. author, tags and
                       other filters
  --issue.resolution                               [string] [default: "empty()"]
  --issue.queue                                                         [string]
  --issue.searchQuery  Startrek query overrides parameters precified in "issue".
                       Query language docs: https://nda.ya.ru/3SdFPJ    [string]

Release existence checks parameters:
  --checks                                  Checks parameters      [default: {}]
  --checks.failOnReleaseBranchExists        Enable check for existing branch
  --checks.failOnReleaseBranchExists.allow  Name patterns for branches that can
  edBranches                                exist when new release is creating
                                                                         [array]
  --checks.failOnReleaseIssueExists         Enable check for existing startrek
                                            issue
  --checks.failOnReleaseIssueExists.allowe  Statuses of existing previous not
  dStatuses                                 closed release issues that can exist
                                            when new release is creating [array]

Options:
  --config
  --help, -h               Show help                                   [boolean]
  --allow-empty-changelog  Create release with empty changelog
                                                      [boolean] [default: false]

Examples:
  $ release create --version=minor

Configuration:

Parameters can be specified in release config.

{
  "issue": {
    "queue": "SEAREL",
    "tags": "report-templates",
    "summary": "si/frontend@ydo/{{version}}"
  },
  "checks": {
    "failOnReleaseBranchExists": {
      "allowedNames": ["**exp**"]
    },
   "failOnReleaseIssueExists": {
      "allowedStatuses": ["Open"]
    }
  }
}

Parameters can be passed as command arguments, e.g:

$ release create --issue.assignee=release-manager
--issue.followers=release-manager
```