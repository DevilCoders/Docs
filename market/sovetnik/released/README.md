# Released

`rlsd` CLI creates a comment about your *release*.

## Installation

1. go to [releases page](https://github.yandex-team.ru/vkozelsky/released/releases) page
2. run command from the particular release in your Terminal

## Requirements

This CLI utility requires your personal token for tracker. You can get one from [wiki](https://wiki.yandex-team.ru/tracker/api/#avtorizacija) page.

After that export your token in `.zshrc` or `.bash_profile`:

```console
export RELEASED_TOKEN=<YOUR_TOKEN_VALUE>
```

## Quick start

```console
rlsd 12345 -d
```

where `12345` is a task id in **SOVETNIK** queue.

Flag `-d` will output your comment to _stdout_.

If you omit `-d` flag, comment will be posted to STARTREK as a comment.

## Usage

```console
USAGE:
    rlsd [FLAGS] [OPTIONS] [Task id] [SUBCOMMAND]

ARGS:
    <Task id>    Task id value

FLAGS:
    -d, --dry-run    Prints a comment to stdout
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -e, --experiment <A/B name, groups>
            Sets an experiment name and groups values, use comma for multiple values

    -s, --sandbox <Sandbox task ids>       Sandbox task id value(s)

SUBCOMMANDS:
    date       Prints current date in a human readable format
    default    Creates a comment with all available fields
    help       Prints this message or the help of the given subcommand(s)
    report     Prints all releases for the current week
    slack      Prints a special comment for Slack
```

## Commands and options

## Help

```console
rlsd
```

or

```console
rlsd -h
```

### Experiment

If you want to provide an info about current A/B:

```console
rlsd 12345 -e ab_name,group_one,group_two,group_n
```

It will create additional sections in your comment:

```console
**TARGETING:** %%202106051652%%

**A/B:** %%ab_name%%

**GROUPS:**
- %%original/control%%
- %%group_one%%
- %%group_two%%
- %%group_n%%
```

### Sandbox link

If you want to provide links to sandbox tasks:

```console
rlsd 12345 -s 1,2,3
```

where `1`, `2`, `3` are sandbox task ids.

### Default comment

Create a comment with all possible fields:

```console
rlsd default
```

Output:

```console
**RELEASED** %%Sat,  5 Jun 2021 16:52:30%%
----

**TARGETING:** %%202106051652%%

**A/B:** %%example_ab%%

**GROUPS:**
- %%original/control%%
- %%group_name%%

**LINKS**
- %%backend%%   <link value>
- %%static%%    <link value>
- %%mobile%%    <link value>
- %%redir%%     <link value>
- %%settings%%  <link value>
- %%landings%%  <link value>
- %%sandbox%%   <link value>
```

Copy this comment to clipboard:

```console
rlsd default -c
```

### Slack

**Slack** command creates a special comment for Slack about current release:

```console
rlsd slack 12345
```

where `12345` is task id in SOVETNIK queue.

If you want to copy a generated message:

```console
rlsd slack 12345 -c
```

### Current date

Print current date:

```console
rlsd date
```

Copy to clipboard:

```console
rlsd date -c
```

### Releases during this week

> Works only with SOVETNIK queue

Show all releases during thise week:

```console
rlsd report
```

If you want to copy a generated message:

```console
rlsd report -c
```

## Working with other queues

`rlsd` can work with two additional queues: `TRAVELFRONT` and `RASPTICKETS`.

The commands are the same but you have to use key and id:

```console
rlsd TRAVELFRONT-12345
rlsd slack TRAVELFRONT-12345
rlsd RASPTICKETS-12345
rlsd slack RASPTICKETS-12345
```
