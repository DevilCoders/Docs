# Как посмотреть конфиг проекта через командную строку

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

- запустите скрипт `get-config`:

  `CLICKHOUSE_PASSWORD=<take it from yav> npm run get-config -- --project <project name>`

  Пароль для доступа к БД ClickHouse возьмите [здесь](https://yav.yandex-team.ru/secret/sec-01dbyvy4fec836rc5h9bqca5x9/explore/version/ver-01dbyvy4fq81xn71y461684pyz).

  Вместо `<project name>` введите имя проекта. Без опции `--project` скрипт вернет конфиг для всех проектов, которые подключены к Тесткопу.

[infratest]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest
