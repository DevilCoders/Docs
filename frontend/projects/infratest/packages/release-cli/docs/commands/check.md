# `release check`

Запускает проверки, чтобы проверить, можно ли создавать новый релиз.

Набор проверок для запуска настраивается в `release.json`.

## Usage

```console
$ npx release check -h

release check

Check whether a new release issue can be created

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

Checking of the possibility of creation is performed using settings specified in
"checks" section of release config file:

"checks": {
    failOnReleaseBranchExists: {
        allowedBranches: []
    },

    failOnReleaseIssueExists: {
        allowedStatuses: ["ReadyForRegress"]
    }
}
```