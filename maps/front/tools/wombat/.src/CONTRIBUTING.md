# Contribution Guide

This document describes some points about contribution process for {{ProjectName}}.

The project is being developed within community. Maintainer merges pull-requests, fixes critical bugs.

## Codestyle

See [Yandex Maps](https://github.com/ymaps/codestyle) and
[inner](https://github.yandex-team.ru/islets/codestyle) codestyle guides.

## Install

Before start installation you have to make sure that there is `yatool` on your local machine.
Read more about this tool [here](https://wiki.yandex-team.ru/yatool/).
To install it please follow [the guides](https://wiki.yandex-team.ru/yatool/distrib/).

### Go to the project work directory

```bash
cd <arcadia-path>/maps/front/services/{{ProjectName}}
# Local machine setup.
make local
# Install i18n
make i18n
# Run dev stand.
make dev
```

The local stand will be available at `https://{{ProjectName}}.dev.c.maps.yandex.ru:8080`.

### Solve any problems

#### Hosts/inthosts

If you need to download ```hosts/inthosts``` packages, run the command

```bash
make hosts
```

It puts these resources to `./sandbox-resources/(int)hosts`.

#### i18n

If you need to update translations from tanker, run
```bash
make i18n
```

## Pull-requests

If you fixed or added something useful to the project, you can send pull-request.
It will be reviewed by maintainer and accepted, or commented for rework, or declined.

## Bugs

If you found an error, mistype or any other flawback in the project, please report about it.
The more details you provide, the easier it can be reproduced and the faster can be fixed.
Unfortunately, sometimes the bug can be only reproduced in your project or in your environment,
so maintainers cannot reproduce it. In this case we believe you can fix the bug and send us the fix.

## Features

It you've got an idea about a new feature, it's most likely that you have do implement it on your own.
If you cannot implement the feature, but it is very important, you can report,
but expect it be declined by the maintainer.

## Deploy

The project has at least two environments: `testing` and `production`.
To release `testing` environment run the following command:

```bash
make release-testing
```

The `production` environment usually never gets released before `testing`, so assuming the current version of `testing`
is already released, the `production` environment can be deployed via:

```bash
make deploy-production
```
