# Yasm-common-project-vars

Made with (@yandex-int/bean)[https://github.yandex-team.ru/maps/infra/tree/master/packages/bean].

Updates the data for the template [maps-front-common-project-vars](https://yasm.yandex-team.ru/srvambry/tmpl/panels/render_json/maps-front-common-project-vars) in yasm. This template is used in all maps frontend Panels/Graphics/Alerts.

## General information
| Key | Value |
|---|---|
| Nirvana | https://nirvana.yandex-team.ru/flow/9e21896c-bb79-474f-938d-852d9e496876/ |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/yasm-common-project-vars |
| Yasm template | https://yasm.yandex-team.ru/srvambry/tmpl/panels/render_json/maps-front-common-project-vars |

## Local setup
1. Switch work directory by `arc` to `maps/front/schedulers/yasm-common-project-vars`.
2. Set up required secrets from [Secrets](#secrets) section.
3. Switch to the actual Node.JS version: `nvm use`.
4. Install dependencies: `npm i`.
5. Run `npm run build && node out/index.js`.

<div id="secrets" />

## Secrets
| Secret | Description |
| ------ | ----------- |
| ABC_OAUTH_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=23db397a10ae4fbcb1a7ab5896dc00f6) for [ABC Api](https://abc-back.yandex-team.ru/api/swagger/) |
| DCTL_YP_TOKEN | [OAuth token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7) for [YP Api](https://wiki.yandex-team.ru/yp/) |
| AWACS_OAUTH_TOKEN | Click on [the lock](https://jing.yandex-team.ru/files/flack/2019-03-14_18-04-02.png) icon near buttons "Create namespace" on [this page](https://nanny.yandex-team.ru/ui/#/awacs) to get OAuth token for [Awacs Api](https://wiki.yandex-team.ru/awacs/api/)

1. Get yours tokens by `OAuth token` links above.
2. For each token copy value of field `access_token` or similar field.
3. Use this template for configurate environment variables:
```shell
ABC_OAUTH_TOKEN='your_token'
DCTL_YP_TOKEN='your_token'
AWACS_OAUTH_TOKEN='your_token'
```

## How it works

1. Take data from [Deploy](https://deploy.yandex-team.ru/), [ABC](https://abc.yandex-team.ru/), [AWACS](https://nanny.yandex-team.ru/ui/) for all maps frontend projects.
2. Update [maps-front-common-project-vars](https://yasm.yandex-team.ru/srvambry/tmpl/panels/render_json/maps-front-common-project-vars) template.

If environment variable `NODE_ENV=production` is set, then the yasm template will be updated, otherwise the result will be written to a local file.

## What happens if scheduler is down

Data for all maps frontend Panels/Graphics/Alerts may be outdated.

## Release

If you want release new version:

```sh
arc checkout -b <branch-name>
npm version <patch|minor|major>
arc add .
arc commit -m "yasm-common-project-vars@<new-version>"
arc pr create
```

Merge your PR via Arcanum.
After merge lama-sync update version in Reactor.
