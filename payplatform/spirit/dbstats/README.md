### Darkspirit-dbstats
Сервис монитринга БД DarkSpirit-а через запросы в базу.

### Техническое устройство сервиса
Сервис основан на библиотеке `mail/python/theatre`, а точнее на скелете приложения
`mail/python/theatre/stages/db_stats`.

Приложение собирает состояние запросами в БД, формирует из результатов метрики, отдает их в ручке `/solomon`.
Запущенный на соседнем box-е `solomon-agent` собирает метрики, за которыми приходит Solomon.
Для самого `solomon-agent` используется образ, собранный коллегами из Биллинга по правилам из `billing/host/scripts/solomon`.

### Настройка в Solomon
В Соломоне заведены следующие сущности:
* Solomon-сервис
  [dbstats](https://solomon.yandex-team.ru/admin/projects/trust_cashregisters/services/trust_cashregisters_dbstats)
  хранит общие настройки работы с метриками: правила агрегации, TTL хранения данных и т.д.
* Solomon-кластеры
  [testing](https://solomon.yandex-team.ru/admin/projects/trust_cashregisters/clusters/trust_cashregisters_deploy_test)
  и
  [production](https://solomon.yandex-team.ru/admin/projects/trust_cashregisters/clusters/trust_cashregisters_deploy_prod)
  задают связь с машинами, на которых запущено приложение - они адресуются через `YP Deploy Unit`, например `spirit-testing.dbstats`
* Solomon-шарды
  [testing](https://solomon.yandex-team.ru/admin/projects/trust_cashregisters/shards/trust_cashregisters_deploy_test_dbstats)
  и
  [production](https://solomon.yandex-team.ru/admin/projects/trust_cashregisters/shards/trust_cashregisters_deploy_prod_dbstats)
  явно фиксируют "разрешенные" сочетания `service + cluster`, для которых имеет смысл обработка метрик.

### Выкатка
Сервис живет в Деплое:
* [testing](https://deploy.yandex-team.ru/stages/spirit-testing/config/du-dbstats)
* [production](https://deploy.yandex-team.ru/stages/spirit-production/config/du-dbstats)

Для выкатки приложения нужно:
* Зайти в [CI](https://a.yandex-team.ru/projects/spirit/ci/releases/timeline?dir=payplatform%2Fspirit%2Fdbstats&id=darkspirit-dbstats-release)
* Выбрать нужный коммит (обычно последний, верхний) и запустить релиз, или же просто нажать на кнопку `Run release` справа сверху
