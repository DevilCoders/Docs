# expenses-processor
Загрузка и процессинг расходов

Флоу работы:

![summaryreport](expenses-processor.svg)

# Краткое описание тасок:
### (Yandex|Customer)(facebook|google|googleSkAd)ConnectorsProcessingEnqueueTask
Таски создают задачи на автоматическую выгрузку коннекторов, но не чаще раза в день. Задачи на выгрузку
яндексовых коннекторов создаются каждый день в ~3 утра, чтобы данные за предыдущий день
успели доехать. Коннекторы пользователей выгружаются через 24 часа после предыдущей выгрузки.
### (facebook|google|googleSkAd)CabinetDownloadingEnqueueTask
Создает задачи на загрузку данных в ydb. Для каждого коннектора находит список выгружаемых
кабинетов, и создает задачи для выгрузки кабинета для каждой даты. Яндексовые кабинеты находит
путем хождения в апи, а для пользовательских идет в таблицу `ads_cabinets`.
### (facebook|google|googleSkAd)CabinetDownloadingTask
Получает на вход от Runner-таски задачи на скачивание кабинетов, группирует их в непрерывные
отрезки времени для уменьшения количества запросов в апи и загружает данные в ydb. После
успешной выгрузки всего коннектора, проставляет статус `DOWNLOADED` коннектору.
## (facebook|google|googleSkAd)ConnectorsYdbToYtTask
Выбирает задачи на выгрузку коннекторов в статусе `DOWNLOADED` и выгружает данные по ним из
ydb в yt.
## (facebook|google)ProcessingTask
Обрабатывает задачи на выгрузку кабинетов в статусе `DOWNLOADED`, получает загруженные данные
из ydb кладет их в s3, а также формирует загрузки в таблице `pg.uploadings.expense_uploadings`
##ExpenseProcessorTask
Обрабатывает загрузки из `pg.uploadings_expense_uploadings` кладет данные в clickouse и в YDB.

## Графики
[Дашбоард expenses-processor](https://grafana.yandex-team.ru/d/N5Pu3jrZz/metrika-expenses-processor?orgId=1&from=now-6h&to=now)
