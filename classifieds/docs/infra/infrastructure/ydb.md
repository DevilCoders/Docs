# YDB

YDB - распределенная база данных с SQL-интерфейсом и ACID-транзакциями.

[Официальная документация](https://ydb.yandex-team.ru/docs/)
[Чат поддержки](https://t.me/joinchat/AqgqJEnmMtiBfXmAeu5HlQ)
[Чат вертикалей про YDB](https://t.me/joinchat/VzTImyZqODi6XRrk)

## Как завести базу

Для тестинга можно использовать коммунальную базу `/ru-prestable/verticals/testing/common` в ABC-проекте **verticals**.

Для прода необходимо заполнить [форму](https://forms.yandex-team.ru/surveys/45941/).
Манипуляции с созданной базой также проводятся через форму: [изменение](https://forms.yandex-team.ru/surveys/30510/), [удаление](https://forms.yandex-team.ru/surveys/30513/).

## Метрики 

Часть метрик есть в [админке облака](yc.yandex-team.ru) на вкладке Monitoring.

Более подробный дашборд доступен в [Соломоне](https://solomon.yandex-team.ru/?project=kikimr&service=kqp&cluster=ydb_ru_prestable&database=%2Fru-prestable%2Fverticals%2Ftesting%2Fcommon&host=cluster&slot=cluster&dashboard=kikimr-mt-database-overall&b=1d&e=).

## Настройка прав

Для операций с базой необходимо получить [права доступа](https://ydb.yandex-team.ru/docs/getting_started/start_auth). Для прода их можно попросить у ответственного за базу (указывается в заявке на создание), для тестинга у своего тимлида.

Для того, чтобы работать с базой из UI админки облака, необходимо иметь роль в скоупе **Управление базами данных** или **Администрирование** в соответствующем ABC-сервисе. 

## Best practices

1) Внимательно изучите документацию. При внешней схожести база очень сильно отличается от классических СУБД типа MySQL и PostgreSQL. 
2) Тщательно проектируйте схему, чтобы избежать проблем с масштабированием. В частности необходимо правильно выбирать [первичный ключ](https://ydb.yandex-team.ru/docs/best_practices/pk_scalability).
3) Проверяйте [план выполнения запросов](https://ydb.yandex-team.ru/docs/reference/ydb-cli/commands/explain-plan?). Не все запросы одинаково эффективны, очень легко получить fullscan и деградировать производительность.
4) Для поиска проблемных запросов/шардов пользуйтесь **Диагностикой** в админке базы.
5) Не используйте личные токены. Создавайте роботов или аутентифицируйтесь через TVM.
