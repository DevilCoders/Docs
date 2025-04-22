Guidelines
==========

_Made with [@yandex-int/bean](https://a.yandex-team.ru/arc_vcs/maps/front/packages/bean)._

Guidelines to check all maps frontend projects with our rules.

## General information

| Key | Value |
|---|---|
| Docs | https://docs.yandex-team.ru/maps-front-guidelines/ |
| Nirvana | https://nirvana.yandex-team.ru/flow/9e21896c-bb79-474f-938d-852d9e496876/ |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/guidelines |

## Local setup
1. Switch work directory by `arc` to `maps/front/schedulers/guidelines`.
2. Set up required secrets from [Secrets](#secrets) section.
3. Switch to the actual Node.JS version: `nvm use`.
4. Install dependencies: `npm i`.

<div id="secrets" />

## Secrets
| Secret | Description |
| ------ | ----------- |
| ABC_OAUTH_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=23db397a10ae4fbcb1a7ab5896dc00f6) for [ABC Api](https://abc-back.yandex-team.ru/api/swagger/) |
| ARCANUM_API_OAUTH_TOKEN | [OAuth token](https://a.yandex-team.ru/api/token) for [Arcanum API](https://a.yandex-team.ru/api/swagger/) |
| DCTL_YP_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7) for [YP Api](https://wiki.yandex-team.ru/yp/) |
| PUNCHER_API_OAUTH_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=a4b9cc023f7244e8b2c7b4fa47c444a6) for [Puncher Api](https://wiki.yandex-team.ru/noc/nocdev/puncher/api/) |
| NIRVANA_OAUTH_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=637ca17604cb4dfa90b262952c00b1e9) for [Nirvana Api](https://wiki.yandex-team.ru/nirvana/components/api/) |
| STARTREK_OAUTH_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b) for [Startrek Api](https://st-api.yandex-team.ru/docs/) |
| JUGGLER_OAUTH_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0) for [Juggler Api](https://juggler.yandex-team.ru/doc//) |
| YT_OAUTH_TOKEN | [OAuth token](https://oauth.yt.yandex.net/) for [YT Api](https://yt.yandex-team.ru/docs/api/commands.html) |
| AWACS_OAUTH_TOKEN | Click on [the lock](https://jing.yandex-team.ru/files/flack/2019-03-14_18-04-02.png) icon near buttons "Create namespace" on [this page](https://nanny.yandex-team.ru/ui/#/awacs) to get OAuth token for [Awacs Api](https://wiki.yandex-team.ru/awacs/api/)

1. Get yours tokens by `OAuth token` links above.
2. For each token copy value of field `access_token` or similar field.
3. Use this template for configurate `.env` file:
```shell
ABC_OAUTH_TOKEN='your_token'
ARCANUM_API_OAUTH_TOKEN='your_token'
DCTL_YP_TOKEN='your_token'
PUNCHER_API_OAUTH_TOKEN='your_token'
NIRVANA_OAUTH_TOKEN='your_token'
STARTREK_OAUTH_TOKEN='your_token'
JUGGLER_OAUTH_TOKEN='your_token'
YT_OAUTH_TOKEN='your_token'
AWACS_OAUTH_TOKEN='your_token'
```

## How to check a single slug
```sh
TARGET=SERVICES:maps-front-maps npm start
```

## How to check only single system (SERVICES, REACTOR, YT)

```sh
TARGET=SERVICES npm start
```

## How to run only a single test or a single suite
In the project we use `mocha`, so `.only` and `.skip` are supported and they are applied globally.
To run a single test just add `.only` to the `check()` call:
```javascript
check.only('DOCKERFILE_EXISTS', () => {...})
```

To run only a single suite:
```javascript
config.runForServices('DOCKERFILE', () => {...}, true)
```

## How to run autofix for a rule

You can run autofix for a specific rule by specifying `AUTOFIX` env variable with the name of the rule:

```sh
AUTOFIX=AWACS_NAMESPACE_ONLY_DEVOPS_ACCESS npm start
```

An autofix for this rule will be executed in dry run mode and change diff will be displayed for each target.

If you want to apply the changes, provide `FORCE=1` env variable:

```sh
AUTOFIX=AWACS_NAMESPACE_ONLY_DEVOPS_ACCESS FORCE=1 npm start
```

## How to enable verbose logging
You can enable verbose logging by passing a env variable to the script:
```sh
ENABLE_LOGGING=1 npm start
```
This will log everything the data providers execute. If you need only `stderr` logs you can always send `stdout` to `/dev/null`:
```sh
ENABLE_LOGGING=1 npm start 1>/dev/null
```

## Docs

You should write JSDoc with `@description` tag before each check in [Markdown format](https://docs.yandex-team.ru/docstools/examples).

On precommit hook your comment will be generated to real Markdown docs.

Example:

```js
/**
 * @description
 * This is **my** rule for real things.
 */
check('MY_RULE', () => {});
```

### How to check docs generating

```sh
npm run docs:generate:local
```

## Release

If you want release new version of guidelines:

```sh
arc pull trunk
arc checkout -b <branch-name>
npm version <patch|minor|major>
arc add .
arc commit -m "guidelines@<new-version>"
arc pr create
```

Wait CI and merge your PR via Arcanum.

After merge `lama-sync` update version of guidelines in Reactor.
