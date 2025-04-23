A tool for mass creating Startrek issues.

Use it as follows:
```
ya make --checkout
export STARTREK_TOKEN=AQAD-your-startrek-token

# won't do anything but print on your stdout:
./startreker <task-id> --dry-run

# will create just one issue
./startreker <task-id>

# and once you're completely sure:
./startreker <task-id> --create-many
```

To obtain the token, visit https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b.

`<task-id>` is the name of a directory inside `./tasks`. It must contain `input.yaml`, a declarative description of the issues to be created:
```json
{
  "required": [
    "meta",
    "issues"
  ],
  "type": "object",
  "properties": {
    "meta": {
      "required": [
        "queue",
        "parent_issue_id",
        "author",
        "tags",
        "followers",
        "summary_template",
        "description_template"
      ],
      "type": "object",
      "properties": {
        "author": {
          "type": "string"
        },
        "summary_template": {
          "type": "string"
        },
        "tags": {
          "items": {
            "type": "string"
          },
          "type": "array"
        },
        "queue": {
          "type": "string"
        },
        "followers": {
          "items": {
            "type": "string"
          },
          "type": "array"
        },
        "description_template": {
          "type": "string"
        },
        "parent_issue_id": {
          "type": "string"
        }
      }
    },
    "issues": {
      "patternProperties": {
        ".*": {
          "required": [
            "assignee",
            "context"
          ],
          "properties": {
            "assignee": {
              "type": "string"
            },
            "invitee": {
              "items": {
                "type": "string"
              },
              "type": "array"
            },
            "context": {
              "type": "object"
            },
            "tags": {
              "items": {
                "type": "string"
              },
              "type": "array"
            }
          }
        }
      },
      "type": "object"
    }
  }
}
```

