# Как обновить конфиг проекта через командную строку

- откройте терминал;

- перейдите в папку проекта [infratest][infratest];

- выполните команды:

  ```
  arc checkout trunk
  arc pull trunk
  ```

- [установите](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest#razrabotka) зависимости;

  _Примечание: не обязательно делать глобальный бутстрап, достаточно установить зависимости только для Тесткопа._

- перейдите в папку `services/testcop`;

## Как установить новое значение конфига

- запустите скрипт `set-config` со следующими опциями:

  ```
  CLICKHOUSE_PASSWORD=<take it from yav> npm run set-config --
    --project <project name>
    --settings <config in JSON-format>
    [--user <user name>]
  ```

  Пароль для доступа к БД ClickHouse возьмите [здесь](https://yav.yandex-team.ru/secret/sec-01dbyvy4fec836rc5h9bqca5x9/explore/version/ver-01dbyvy4fq81xn71y461684pyz).

  Здесь: 
    - `<project name>` – имя проекта.
    - `<config in JSON-format` – значение конфига в JSON-формате.
    - `<user name>` – автор изменений конфига (можно не указывать, по умолчанию: имя текущего пользователя в вашей ОС). 

## Как удалить конфиг

- запустите скрипт `set-config` со следующими опциями:

  ```
  CLICKHOUSE_PASSWORD=<take it from yav> npm run set-config --
    --project <project name>
    --remove
    [--user <user name>]
  ```

## Как синхронизировать конфиг для проекта из пакета testcop-config

На данный момент пока ещё источником правды является пакет [testcop-config][testcop-config]. Чтобы синхронизировать конфиг проекта в базе данных с его конфигом в пакете [testcop-config][testcop-config] запустите скрипт `set-config` со следующими опциями:

```
CLICKHOUSE_PASSWORD=<take it from yav> npm run set-config --
  [--project <project name>]
  --from-testcop-config
  [--user <user name>]
```

Без опции `--project` скрипт обновит конфиг для всех проектов, которые подключены к Тесткопу.

[infratest]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest
[testcop-config]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/testcop-config/index.js
