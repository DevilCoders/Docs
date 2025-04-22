# Summary

`summary` is a CLI utility to create a report with info about projects in development.

## Requirements

- [Access token for API](https://wiki.yandex-team.ru/tracker/api/#avtorizacija)
- Environment variable in your shell: `ST_TOKEN`

### Setup env var

#### macOS

```console
echo "export ST_TOKEN='ST_TOKEN_VALUE'" >> ~/.zshrc && source ~/.zshrc
```

#### Windows

```console
$Env:ST_TOKEN="ST_TOKEN_VALUE"
```

## Flags

### Show list of projects

> Default author of tickets is @wavefront.
> Default date is `today`.

```console
summary
```

#### Author and date

You can set a different author of tickets and a specific date in the following format:

```console
summary -a user_name -d "19.05.2022"
```

#### List formatting

You can change a list formatting. There are two options: Tracker or Telegram.

> Default option is Telegram: `tg`.

Tracker formatting:

```console
summary -f st
```

Telegram formatting:

```console
summary -f tg
```

##### Difference between Tracker and Telegram formatting

Tracker doesn't have project links, full names of assignees because Tracker can parse and create them automatically by using special syntax.

Example:

```md
**Разработка выделена полностью**

PROJECT-ID-1:
- staff:name с `2022-06-13`

PROJECT-ID-2:
- staff:name с `2022-06-13`

**Остальные проекты**

PROJECT-ID-3:
- staff:name с `2022-06-13`
```

Telegram has a lot of additional info:

```md
**Разработка выделена полностью**

PROJECT-ID-1: Project summary
Project link
- Name Surname с `2022-06-13`

PROJECT-ID-2: Project summary
Project link
- Name Surname с `2022-06-13`

**Остальные проекты**

PROJECT-ID-3: Project summary
Project link
- Name Surname с `2022-06-13`
```

### Help message

```console
summary -h
```

```console
summary --help
```

## Build

```console
go build
```

### Build for specific OS

Windows:

```console
GOOS=windows go build
```
