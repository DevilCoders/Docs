# Contribution Guide

This document describes some points about contribution process for cartograph.

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

### How to start
1. [Install node.js](https://nodejs.org/en/download)

2. Export secrets to your `$HOME/.bashrc` or `$HOME/.bash_profile` file: [`QTOOLS_TOKEN`](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4dd38b9acbb44ad8a7ece163ddf1c53a), [`TANKER_OAUTH_TOKEN`](https://nda.ya.ru/3SjQY7).

3. Build application
    ```sh
    nvm use
    npm ci
    npm run setup
    ```

4. Run application
    ```sh
    npm start
    # Or on other port:
    PORT=3000 npm start
    ```

5. Оpen `https://$(user-name).cartograph.dev.yandex-team.ru:8080`

> Don't forget about to trust certificate, [instruction to trust](https://wiki.yandex-team.ru/sigorilla/crt-hsts/).
>
> With out this local stand may not work.

### How to deploy
```sh
npm run release:testing
```

### How to check codestyle, jsdoc and styles
```sh
npm run lint
```

## How to test

Warning: You need a working stand to run tests.

```
npm run test:func

or

MATCH='{string identifier here}' npm run test:func
```
Example: `MATCH='Diffs view.' npm run test:func`

### Look also
* [Docs](docs/README.md)
