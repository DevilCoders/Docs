# Contributing

The maintainer accepts pull requests and has the right to reject them if they does not meet project's standards.
If you have a bug report or a feature request, please use the project's
[task queue](https://github.yandex-team.ru/maps/infra/issues).
First try to find if your issue already exits, if not you can create an issue. If your issue involves developing code, you might be asked for contribution.
Before writing any code, please take a look at the [codestyle](https://github.com/ymaps/codestyle) used in the codebase.
Before sending your pull request, please check that the list tools and the unit tests pass.

## Requirements

* [Node.js](http://nodejs.org/) `6`
* [npm](http://npmjs.org) `3`
* `QTOOLS_TOKEN` as environment variable

## Run tests

```sh
npm install
npm test
```

## Run e2e test

```sh
npm run e2e
```

## Release

Please, don't forget to write changes in [CHANGELOG.md](CHANGELOG.md) before release.

```sh
npm version (patch | minor | major)
git push origin master --follow-tags
npm publish
```
