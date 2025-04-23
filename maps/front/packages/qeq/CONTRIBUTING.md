# Contributing

The maintainer accepts pull requests and has the right to reject them if they does not meet project's standards.
If you have a bug report or a feature request, please use the project's
[task queue](https://github.yandex-team.ru/maps/qeq/issues).
First try to find if your issue already exits, if not you can create an issue. If your issue involves developing code, you might be asked for contribution.
Before writing any code, please take a look at the [codestyle](https://github.com/ymaps/codestyle/blob/master/typescript.md) used in the codebase.
Before sending your pull request, please check that the list tools and the unit tests pass.

## Requirements

* [node.js](http://nodejs.org/) `8`, use NVM for currect version: `nvm use`.
* [npm](http://npmjs.org) `6`
* [`QTOOLS_TOKEN`](https://github.yandex-team.ru/maps/qtools#authorization) as environment variable

## Build project

```sh
npm install
npm run build
```

## Release

```sh
npm version (patch | minor | major)
git push origin master --follow-tags
npm publish
```
