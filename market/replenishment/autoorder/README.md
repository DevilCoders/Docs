# API для автозаказов

## Настройка IDEA
- Установить плагин lombok

## Запуск через local-start script
```$bash
ya make && ./bin/autoorder-local-start.sh
```

## [Курс молодого бойца](https://wiki.yandex-team.ru/market/replenishment/interface/kurs-molodogo-bojjca/)
## [Подготовка локального окружения для разработки Autoorder](https://wiki.yandex-team.ru/market/replenishment/interface/Replenishment/)

## Возможные ошибки при запуске и способах их решения
- Если возникает `Failed to init TVM2.0 ServiceContext: java.lang.UnsatisfiedLinkError: no ticket_parser2_java in java.library.path` ошибка при старте приложения,
 то необходимо скачать [этот](https://yadi.sk/d/NfovMLwLk2jI6A)
 архив и положить оба файла из него туда, где джава их увидит (например, /usr/lib/ для линукса),
 затем обновить кэш статических библиотек выполнив sudo ldconfig.
 Для mac OS готовую библиотеку можно скачать [тут](https://wiki.yandex-team.ru/users/mors741/tvm-ticketparser2java-lib-from-sources/#gotovajalibapodmacos), положить ее надо в /Library/Java/Extensions

## Структура приложения
Важная часть приложения - загрузка данных из YT. Для отслеживания появления таблиц в YT используется
механизм Step Events (https://wiki.yandex-team.ru/sandbox/step/). Классы для работы со Step API лежат в пакете
`ru.yandex.market.replenishment.autoorder.step`. События забираются раз в 5 минут по всем табличка через `YtTableWatchService`
и складываются в табличку `yt_table_watch_log`

Так называемые лоадеры из пакета `ru.yandex.market.replenishment.autoorder.service.yt.loader` смотрят в табличку `yt_table_watch_log`
и для каждого необработанного события выполняют загрузку таблицы из YT в соответствующую таблицу Postgre.

Конфигурации приложения находятся в пакете `ru.yandex.market.replenishment.autoorder.config`

Доменные объекты и репозитории находятся соответственно в пакетах `ru.yandex.market.replenishment.autoorder.model`
и `ru.yandex.market.replenishment.autoorder.repository`. Внутри них есть подразделение на классы для работы с PDB и Postgres.

Контроллеры приложения можно найти в пакете `ru.yandex.market.replenishment.autoorder.api`

## Генерация файла definitions.ts для фронта
Запускаем генерацию
`ya.make definitions`
После чего создается архив _definitions/autoorder-definitions.jar_,
в нем лежит файл _definitions.ts_.

Более подробную информацию можно найти [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/springmvc-to-ts)

## Различные ссылки
Продакшн сервисы в RTC:
https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_autoorder_iva/
https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_autoorder_vla/

Тестинг:
https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_autoorder_sas/
https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_autoorder_vla/

Релизный пайплайн:
https://tsum.yandex-team.ru/pipe/projects/replenishment/delivery-dashboard/autoorder

Фолдер с PostgreSQL в MDB:
https://yc.yandex-team.ru/folders/foo2u5pfn5s7or3qenu8/managed-postgresql

Секреты:
`autoorder_secrets_testing` и `autoorder_secrets_production` на https://yav.yandex-team.ru (скрытые, просите доступа)

Проект в Solomon (тут пытались построить какие-то графики):
https://solomon.yandex-team.ru/?project=market-managementsystems
