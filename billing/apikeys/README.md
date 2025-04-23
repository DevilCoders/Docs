# Apikeys

Кабинет разработчика - это сервант выдачи ключей, в первую очередь, пользователям API сервисов Яндекса.
Цель Кабинета: обеспечить выдачу ключей к открытым наружу API сервисов Яндекса в одном месте, обеспечить выдачу и биллинг платных ключей.

[Проект в ABC](https://abc.yandex-team.ru/services/developer/)

## Разработка

`svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone`

`cd arcadia`

Сборка `./ya make --checkout -j8 billing/apikeys`

Запуск тестов `./ya make -tt billing/apikeys`

Запуск сервера
```bash
YANDEX_XML_CONFIG=billing/apikeys/uwsgi_backend/balance-apikeys-uwsgi-backend.cfg.xml \
billing/apikeys/uwsgi_backend/balance_apikeys_uwsgi_backend_app -w billing.apikeys.uwsgi_backend.balance_apikeys_uwsgi_backend_app --http-socket :8080
```
