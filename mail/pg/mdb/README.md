# maildb

https://st.yandex-team.ru/STORAGE-146

Мы используем 9 [схем](https://www.postgresql.org/docs/current/static/sql-createschema.html).

Схемы с данными:

 1. mail - письма, папки и метки
 2. filters - фильтры (данные для [furita](https://wiki.yandex-team.ru/mail/furita/))
 3. mailish -  данные для [xeno](https://wiki.yandex-team.ru/Pochta/mx/xeno/db/)
 4. constraints - функции для описания версий метаданных пользователя [MAILDEV-448](https://st.yandex-team.ru/MAILDEV-448)
 5. stats - статистика её строят `dba`
 6. ora - mapping-ги перенесённых идентификаторов
 7. settings - пользовательские настройки

Схемы с процедурами:

 8. impl - внутренние процедуры
 9. code - процедуры
 10. utils - процедуры для `dba`


* [cron](/python/cron/README.md)
* pymdb - обвязки для запросов и миграции вокруг code.\*
* [tests](/tests/README.md) - тесты для процедур

[Полезные запросы](mail-magic.md)

[Про миграции](https://wiki.yandex-team.ru/mail/pg/xdb/migrations/)
