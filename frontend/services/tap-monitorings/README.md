# Проверки (checks) Juggler

Общая конфигурация всех чеков Juggler хранится в `.monitorado.yml`.

Для обновления необходимо:

-   установить зависимости

```bash
npx lerna bootstrap --scope @yandex-int/tap-monitorings
```

-   получить OAuth токен для Monitorado [по ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=171fcece39a04fd0a6b8b74950336008)
-   скопировать полученный токен и подставить в команду вместо `OAUTH_TOKEN`

```bash
npm config set @yandex-int/tap-monitorings:monitorado_token OAUTH_TOKEN
```

-   поправить конфиг (по необходимости)
-   посмотреть отличие от текущего:

```bash
npx lerna run diff --scope @yandex-int/tap-monitorings --stream
```

-   обновить чеки:

```bash
npx lerna run update --scope @yandex-int/tap-monitorings --stream
```

# Мониторинги TAP в Juggler

Общая конфигурация панели Juggler - `.juggler_board.yml`

-   [Готовая панель Production](https://juggler.yandex-team.ru/dashboards/tap/)
-   [Готовая панель Testing](https://juggler.yandex-team.ru/dashboards/tap-test/)
-   [Готовая панель TV](https://juggler.yandex-team.ru/dashboards/tap-tv/)

# Панели TAP в YASM

Общая конфигурация шаблона панели YASM - `.yasm.main.jinja`

-   [Шаблон панели Production](https://yasm.yandex-team.ru/template/panel/tap/)
-   [График агрегированных данных по всем сервисам](https://yasm.yandex-team.ru/template/panel/tap/upstream=services/)
-   [График всех сервисов Production](https://yasm.yandex-team.ru/template/panel/tap/upstream=services_production_list/)
-   [График всех сервисов Testing](https://yasm.yandex-team.ru/template/panel/tap/upstream=services_testing_list/)

## Для работы требует

```bash
upstream=<upstream>
```

## Все upstream'ы

```bash
upstream=services # агрегация по всем сервисам
```

## С помощью `geo_spread` можно разложить графики по DC

```bash
upstream=services; geo_spread=yes
```

# Чат мониторингов

-   [Telegram](https://t.me/joinchat/B9JKrliyX8UpmFRl6SqhZw)

# Полезные ссылки

-   [Дока по Juggler](https://wiki.yandex-team.ru/sm/juggler/)
-   [Дока по Головану (yasm)](https://wiki.yandex-team.ru/golovan/)
-   [Дока по шаблонам панелей Голована](https://wiki.yandex-team.ru/golovan/templatium/writing/)
-   [Дока по monitorado](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/monitorado/README.md)
