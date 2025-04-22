# Contribution Guide

This document describes some points about contribution process for spec-admin.

The maintainer of the project is artemsavossin <artemsavossin@yandex-team.ru>.
The ex-maintainer of the project is tgnc <tgnc@yandex-team.ru>.

The project is being developed within community. Maintainer merges pull-requests, fixes critical bugs.

## Codestyle

* [TypeScript](https://github.com/ymaps/codestyle)
* [HTTP API](https://wiki.yandex-team.ru/tech/APIunification/#httpapi)

## Pull-requests

If you fixed or added something useful to the project, you can send pull-request.
It will be reviewed by maintainer and accepted, or commented for rework, or declined.

## Bugs

If you found an error, mistype or any other flawback in the project, please report about it using github-issues.
The more details you provide, the easier it can be reproduced and the faster can be fixed.
Unfortunately, sometimes the bug can be only reproduced in your project or in your environment,
so maintainers cannot reproduce it. In this case we believe you can fix the bug and send us the fix.

## Features

It you've got an idea about a new feature, it's most likely that you have do implement it on your own.
If you cannot implement the feature, but it is very important, you can add a task in github-issues,
but expect it be declined by the maintainer.

## Deploy

This project uses [qtools](https://github.yandex-team.ru/maps/qtools) to interface with docker, the
docker registry and the [Y.Deploy](https://deploy.yandex-team.ru/) cloud platform.

### Release to testing

```sh
make patch # or minor, major
arc pr create --push
```

Merge new PR after all checks. Pull trunk. Then create and push new release tag:

```sh
make arc-tag
```

### Deploy the current version to production

```sh
./node_modules/.bin/qtools deploy production
```
