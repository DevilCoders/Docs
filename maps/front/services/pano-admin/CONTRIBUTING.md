# Contribution Guide

This document describes some points about contribution process for pano-admin.

The project is being developed within community. Maintainer merges pull-requests, fixes critical bugs.

## Codestyle
See [Yandex Maps](https://github.com/ymaps/codestyle) and [inner](https://github.yandex-team.ru/maps/maps/blob/master/codestyle.md) codestyle guides.

## Install

### Choose any directory

```
git clone git@github.yandex-team.ru:maps/pano-admin.git ~/www/pano-admin
cd ~/www/pano-admin
```

### Local machine setup

```
npm run local-setup
```
There were some issues with ssl keys generation, the details can be found [here](https://forum.laragon.org/topic/1600/err_ssl_key_usage_incompatible-default-ssl-in-laragon/5). 

##  Run

```
npm run dev
```
Go to `https://<username>.panoadmin.dev.yandex-team.ru:8080`.

## Pull-requests

Please remember the project uses [git-flow](https://nvie.com/posts/a-successful-git-branching-model/) branching model.
If you fixed or added something useful to the project, you can send pull-request.
It will be reviewed by maintainer and accepted, or commented for rework, or declined.

## Bugs

If you found an error, mistype or any other drawback in the project, please report about it using github-issues.
The more details you provide, the easier it can be reproduced and the faster can be fixed.
Unfortunately, sometimes the bug can be only reproduced in your project or in your environment,
so maintainers cannot reproduce it. In this case we believe you can fix the bug and send us the fix.

## Features

It you've got an idea about a new feature, it's most likely that you have to implement it on your own.
If you cannot implement the feature, but it is very important, you can add a task in github-issues,
but expect it to be declined by the maintainer.

## Unit testing

Run unit test
```
npm run test
```

When you create a new component's test case, snapshot creates auto in first run.

If you changed render of React's component and your snapshot changes expected:
Update React components snapshots
```
npm run test:update-snapshots
```

Debug unit test via Chrome console (open chrome://inspect and choose Node)
```
npm run test:debug
```

If you want to add unit test for component/module, you should create in same folder new file `{filename}.test.ts(x)`.
