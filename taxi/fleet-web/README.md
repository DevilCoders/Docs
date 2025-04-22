# Fleet Web

[![testing][testing_status_icon]][teamcity_testing]
[![auto_release][auto_release_status_icon]][teamcity_auto_release]
[![Dependencies status](https://badger.yandex-team.ru/oko/repo/taxi/fleet-web/health.svg)](https://oko.yandex-team.ru/repo/taxi/fleet-web)

- [Versions](#versions)
- [Infrastructure](#infrastructure)
- [Configs](#configs)
- [Contributing](#contributing)
- [Env variables](#env-variables)
- [Testing](#testing)
- [Code style](#code-style)
- [Localization](#localization)
- [Commit messages](#commit-messages)

## Versions

| Version     | Testing                             | Production                                                      |
| ----------- | ----------------------------------- | --------------------------------------------------------------- |
| Yandex      | [fleet.tst.yandex.ru][]             | [fleet.yandex.ru][], [fleet-web-pre.taxi.yandex.ru][]           |
| Yandex-Team | [fleet.tst.yandex-team.ru][]        | [fleet.yandex-team.ru][], [fleet-web-pre.taxi.yandex-team.ru][] |
| Yango       | [fleet-yango.taxi.tst.yandex.net][] | [fleet.yango.com][]                                             |
| Uber        | [fleet-uber.tst.yandex.net][]       | [fleet2.support-uber.com][]                                     |

[fleet.tst.yandex.ru]: https://fleet.tst.yandex.ru
[fleet.tst.yandex-team.ru]: https://fleet.tst.yandex-team.ru/
[fleet-yango.taxi.tst.yandex.net]: https://fleet-yango.taxi.tst.yandex.net/
[fleet-uber.tst.yandex.net]: https://fleet-uber.tst.yandex.net/
[fleet-web-pre.taxi.yandex.ru]: https://fleet-web-pre.taxi.yandex.ru
[fleet-web-pre.taxi.yandex-team.ru]: https://fleet-web-pre.taxi.yandex-team.ru
[fleet.yandex.ru]: https://fleet.yandex.ru
[fleet.yango.com]: https://fleet.yango.com
[fleet.yandex-team.ru]: https://fleet.yandex-team.ru/
[fleet2.support-uber.com]: https://fleet2.support-uber.com/

## Infrastructure

|             | Testing                           | Production                            |
| ----------- | --------------------------------- | ------------------------------------- |
| Nanny       | [Testing][taxi_fleet-web_testing] | [Stable][taxi_fleet-web_stable]       |
| TeamCity    | [Testing][teamcity_testing]       | [Auto Release][teamcity_auto_release] |
| Grafana     | [Testing][grafana_testing]        | [Production][grafana_stable]          |
| YASM        | [Testing][yasm_testing]           | [Production][yasm_production]         |
| MDS S3      | [Testing][s3_testing]             | [Production][s3_production]           |
| CDN         | -                                 | [Production][cdn_production]          |
| Kibana      | [Testing][kibana_testing]         | [Production][kibana_stable]           |
| Tanker      | -                                 | [Production][tanker_production]       |
| Errors      | -                                 | [Production][error_counter]           |
| Metrika     | -                                 | [Production][metrika_production]      |
| Performance | -                                 | [Production][rum_counter]             |
| Dispenser   | -                                 | [Production][dispenser_production]    |

[rum_counter]: https://rum.yandex-team.ru/projects/fleet-web
[error_counter]: https://error.yandex-team.ru/projects/fleet-web
[teamcity_testing]: https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_FleetWeb_CustomTesting
[teamcity_auto_release]: https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_FleetWeb_AutoRelease
[taxi_fleet-web_testing]: https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_fleet-web_testing/
[taxi_fleet-web_pre_stable]: https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_fleet-web_pre_stable/
[taxi_fleet-web_stable]: https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_fleet-web_stable/
[testing_status_icon]: https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:YandexTaxiProjects_Frontend_FleetWeb_CustomTesting)/statusIcon.svg
[auto_release_status_icon]: https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:YandexTaxiProjects_Frontend_FleetWeb_AutoRelease)/statusIcon.svg
[grafana_testing]: https://grafana.yandex-team.ru/d/xxQvX2QZk/nanny_taxi_fleet-web_testing
[grafana_stable]: https://grafana.yandex-team.ru/d/09x892QZk/nanny_taxi_fleet-web_stable
[yasm_testing]: https://yasm.yandex-team.ru/panel/robot-taxi-clown.nanny_taxi_fleet-web_testing
[yasm_production]: https://yasm.yandex-team.ru/panel/robot-taxi-clown.nanny_taxi_fleet-web_stable
[s3_testing]: https://yasm.yandex-team.ru/template/panel/s3_client/bucket=fleet-web;owner=24549;ctype=testing
[s3_production]: https://yasm.yandex-team.ru/template/panel/s3_client/bucket=fleet-web;owner=24549
[cdn_production]: https://cdn-static.yandex-team.ru/projects/s3_fleet/projectDashboard
[metrika_production]: https://metrika.yandex.ru/dashboard?id=65519053
[kibana_stable]: https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(('$state':(store:appState),meta:(alias:!n,disabled:!f,index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,key:ngroups,negate:!f,params:!(taxi_fleet-web_pre_stable,taxi_fleet-web_stable),type:phrases,value:'taxi_fleet-web_pre_stable,%20taxi_fleet-web_stable'),query:(bool:(minimum_should_match:1,should:!((match_phrase:(ngroups:taxi_fleet-web_pre_stable)),(match_phrase:(ngroups:taxi_fleet-web_stable)))))),('$state':(store:appState),meta:(alias:!n,disabled:!f,index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,key:level,negate:!f,params:!(ERROR,WARNING),type:phrases,value:'ERROR,%20WARNING'),query:(bool:(minimum_should_match:1,should:!((match_phrase:(level:ERROR)),(match_phrase:(level:WARNING))))))),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:''),sort:!(!('@timestamp',desc)))
[kibana_testing]: https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:''),sort:!(!('@timestamp',desc)))
[tanker_production]: https://tanker.yandex-team.ru/?project=fleet&branch=master
[dispenser_production]: https://dispenser.yandex-team.ru/db/projects/taxitaxifleetweb

## Configs

| Config                                       | Testing                                         | Production                                        |
| -------------------------------------------- | ----------------------------------------------- | ------------------------------------------------- |
| Fleet Access Control Permissions             | [Testing][fleet_permissions_testing]            | [Production][fleet_permissions_stable]            |
| Fleet Authproxy Access Rules                 | [Testing][fleet_authproxy_access_rules_testing] | [Production][fleet_authproxy_access_rules_stable] |
| Fleet Authproxy Route Rules                  | [Testing][fleet_authproxy_rules_testing]        | [Production][fleet_authproxy_rules_stable]        |
| Dispatcher access control grants by sections | [Testing][dac_grants_by_sections_testing]       | [Production][dac_grants_by_sections_stable]       |
| Fleet UI Brands                              | [Testing][fleet_ui_brands_testing]              | [Production][fleet_ui_brands_stable]              |
| News                                         | [Testing][news_dispa_testing]                   | [Production][news_dispa_stable]                   |
| Notifications                                | [Testing][opteum_notifications_testing]         | [Production][opteum_notifications_stable]         |

Service in [ABC](https://abc.yandex-team.ru/services/taxitaxifleetweb/)

[fleet_authproxy_access_rules_stable]: https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/FLEET_AUTHPROXY_ACCESS_RULES
[fleet_authproxy_access_rules_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/FLEET_AUTHPROXY_ACCESS_RULES
[fleet_authproxy_rules_stable]: https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/FLEET_AUTHPROXY_ROUTE_RULES
[fleet_authproxy_rules_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/FLEET_AUTHPROXY_ROUTE_RULES
[fleet_permissions_stable]: https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/FLEET_ACCESS_CONTROL_PERMISSIONS
[fleet_permissions_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/FLEET_ACCESS_CONTROL_PERMISSIONS
[dac_grants_by_sections_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/DISPATCHER_ACCESS_CONTROL_GRANTS_BY_SECTIONS
[dac_grants_by_sections_stable]: https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/DISPATCHER_ACCESS_CONTROL_GRANTS_BY_SECTIONS
[fleet_ui_brands_stable]: https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/FLEET_UI_BRANDS
[fleet_ui_brands_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/FLEET_UI_BRANDS
[news_dispa_stable]: https://tariff-editor.taxi.yandex-team.ru/news-dispa
[news_dispa_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/news-dispa
[opteum_notifications_stable]: https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/OPTEUM_NOTIFICATIONS
[opteum_notifications_testing]: https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/OPTEUM_NOTIFICATIONS

## Contributing

Clone repo

```shell
git clone git@github.yandex-team.ru:taxi/fleet-web.git
cd fleet-web
```

Install [nvm](https://github.com/nvm-sh/nvm).

```shell
# installation script
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash

# check installation
command -v nvm
# -> nvm
```

Install Node.js version with nvm.

```shell
nvm install
```

Install Yarn binary globally

```shell
npm i -g yarn
```

Install dependencies

```shell
yarn
```

Install and set up [mkcert](https://github.com/FiloSottile/mkcert).

```shell
brew install mkcert
mkcert -install
```

Generate SSL certificates to enable HTTPS for local development.

```shell
yarn app:mkcert
```

Add dev-server domains to your [hosts](<https://en.wikipedia.org/wiki/Hosts_(file)>).

```
0.0.0.0 fleet.localhost.yandex.ru
0.0.0.0 fleet.localhost.yandex.com
0.0.0.0 fleet.localhost.yandex-team.ru
0.0.0.0 fleet-uber.localhost
```

Start the development server

```shell
yarn app:dev
```

Visit one of the following URLs

| Version     | URL                                                                   |
| ----------- | --------------------------------------------------------------------- |
| Yandex      | https://fleet.localhost.yandex.ru, https://fleet.localhost.yandex.com |
| Yandex-Team | https://fleet.localhost.yandex-team.ru                                |
| Uber        | https://fleet-uber.localhost                                          |

## Env variables

[Vite Env Variables and Modes](https://vitejs.dev/guide/env-and-mode.html#env-files)

We use `testing` and `stable` modes.

When you don't pass `--mode` explicitly, `.env` is used.
It's equivalent to `--mode testing` since we don't have `.env.testing` file.

Pass `--mode stable` explicitly to override environment with variables from `.env.stable`.

## Testing

Testing framework is based on [Jest](https://jestjs.io/docs/en/api) and [Enzyme](https://airbnb.io/enzyme/docs/api/).

```shell
yarn jest
```

## Code style

See [CODE_STYLE](docs/CODE_STYLE.md)

## Localization

See [i18n package](packages/i18n/README.md)

## Commit messages

Commit messages are based on Yandex.Taxi [commit message guidelines](https://github.yandex-team.ru/taxi/backend/wiki/Commit-message-guidelines).

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Or you can use `yarn cz` instead of `git commit ...`
