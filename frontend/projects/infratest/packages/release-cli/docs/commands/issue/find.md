# `release issue find`

Находит релизный тикет по указанным параметрам.

## Usage

```console
$ npx release issue find -h

release issue find

Search release issue in Startrek with specified rearch parameters.

Issue search parameters:
  --issue              Startrek issue parameters
  --issue.<parameter>  Startrek filters for find query, e.g. author, tags and
                       other filters
  --issue.resolution                               [string] [default: "empty()"]
  --issue.queue                                                         [string]
  --issue.searchQuery  Startrek query overrides parameters precified in "issue".
                       Query language docs: https://nda.ya.ru/3SdFPJ    [string]

Placeholders:
  --version       Release {{version}} placeholder                       [string]
  --placeholders  Placeholders for configuration values {{key}}: key=value
                                                                         [array]

Options:
  --config
  --help, -h  Show help                                                [boolean]

Examples:
  $ release issue find --issue.queue SEAREL --issue.summary
  something@{{version}} --placeholders version=1

Searching parameters can be specified in release config "issue" section:

"issue": {
    queue: "SEAREL",
    tags: ["report-templates", "monorepo"]
}

All parameters will be added to issue search query.

Parameters can be passed as command arguments, e.g:
find --issue.queue SEAREL --issue.tags "report-templates" --issue.tags
"monorepo"

You can use {{placeholders}} in parameters. Their values must be specified via
--placeholders option.
A placeholder {{version}}, commonly used in the release issue summary, can be
passed through a special option --version.

"issue": {
    queue: "SEAREL",
    summary: {{prefix}}/frontend@{{version}}
}

find --config ./path/to/config --version 123 --placeholders prefix=release
```