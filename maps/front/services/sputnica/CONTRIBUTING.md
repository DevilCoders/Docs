# Contribution Guide

This document describes some points about contribution process for scanex.

The maintainer of the project is Pavel Bocharov <pv-bocharov@yandex-team.ru>.

The project is being developed within community. Maintainer merges pull-requests, fixes critical bugs.

## Codestyle
See [Yandex Maps codestyle](https://github.yandex-team.ru/maps/maps/blob/master/codestyle.md).

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

## How to start

1. [Install node.js](https://nodejs.org/en/download)

2. Prepare environment: run the code below and make steps that described in [article](https://wiki.yandex-team.ru/sigorilla/crt-hsts/)
    ```sh
    npm run local-setup
    ```

2. Prepare for building
    ```sh
    npm i
    npm run i18n
    ```

2. Build and run application
    ```sh
    npm run dev
    ```

4. Оpen `https://sputnica.dev.yandex.ru:8080`

## How to deploy
1. Merge your PR into master branch

2. Raise version (`major.minor.patch`) and make commit

    To raise patch version:
    ```sh
    npm run patch
    ```
    To raise minor version:
    ```sh
    npm run minor
    ```

3. Wait until current tag build and publish

**Note.** If you want, you can build locally and publish
```sh
npm run release-testing
```

## How to check codestyle, jsdoc and styles
```sh
npm run lint
```
