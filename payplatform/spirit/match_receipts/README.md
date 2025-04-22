# Сверки чеков и платежей
Это автоматический процесс сопоставления данных о чеках (Кассы, ОФД) и данных о платежах (Траст, Баланс, etc.).
Основные цели:
- выявление проблем с фискализацией платежей,
- вынос соответствующей логики в [сервис фискализации](https://wiki.yandex-team.ru/users/kirillovap/celevaja-arxitektura-kass/).

## Компоненты

- Код в этом репозитории описывает всю логику сбора, сопоставления и агрегирования данных ([подробнее](#logic));
- [Hitman-процесс](https://hitman.yandex-team.ru/projects/trust_cashes/MR/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20) - запускает граф в нирване, который собирает и запускает этот код ([подробнее](#launch));
- Все данные-результаты работы скрипта [лежат в yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/balance/prod/spirit/receipts_matching/stable) ([подробнее](#data));
- [Дашборд](https://datalens.yandex-team.ru/2v6tik4cp5p8w-sverki-kass) со всеми графиками на основании полученных данных. Данные обновляются раз в сутки, на линейные графики настроены алерты ([подробнее](#charts));
- Запуск сверки происходит от лица робота [`robot-match-receipts`](https://staff.yandex-team.ru/robot-match-receipts). Ему выданы права на чтение всех таблиц необходимых для сверки, а также права на запись в `//home/balance/prod/spirit/receipts_matching`.
- [chyt-клика](https://yt.yandex-team.ru/hahn/operations/94ab80b5-1636d7ff-3fe03e8-8dfc5238/details) в выделенном пуле. На страничке операции есть ссылки на дашборды с метриками клики.

## Как выкатить новую версию
1. Вмерджить в транк. Скопировать номер ревизии. Из интерфейса арканума: History -> Слева от нужного коммита будет что-то вроде "r9657106".
2. В графе сверок (Hitman -> Сверка чеков -> Граф в нирване):
   - создать новую версию (Clone),
   - у кубика сборки проекта из аркадии поменять параметр "Arcadia Revision" на число из пункта 1 (без буквы r!),
   - добавить комментарий для версии (клик по фону под кубиками -> справа вкладка Details -> Comment),
   - Set as main,
   - Для проверки можно ещё раз перейти из интерфейса Hitman, должна сразу открыться новая версия.
3. При необходимости запустить пересчёт сверки за прошедшие дни (из интерфейса Hitman).

## <a name="launch"></a>Запуск сверки

Самый простой способ запустить сверку — воспользоваться триггерами в [Hitman-процессе](https://hitman.yandex-team.ru/projects/trust_cashes/MR/?jobCreationTimeQuery=YEAR&jobPage=1&pageSize=20). Запустить можно всю сверку в целом или только часть направлений (например "Траст-Кассы"), можно выбрать даты, явно задать папку для результатов (полезно если нужно "досчитать" зафейлившуюся сверку).

Команда запуска "всей сверки" (так можно запустить локально):
```commandline
./match_receipts --start_date '2021-08-13' --end_date '2021-08-25' --yql_token "$(cat /path/to/yql_token)" --tm_token "$(cat /path/to/tm_token)" --default_base_yt_dir //tmp/some_path --hahn_base_yt_dir //home/balance/prod/spirit/receipts_matching/stable match publish
```
Токены можно выписать на себя (у `Разработки ККТ` есть все нужные доступы) или взять роботные из секретницы/нирваны.

В консоль (в нирване прорастет в логи кубика) будет писаться информация о текущем состоянии всех запущенных job-ов с указанием пути к вычисляемой таблице, а также ссылки на job-у в интерфейсе YQL/TM. Примерно так:
```commandline
2021-08-26 11:36:50,994 INFO YQL operation started: https://yql.yandex-team.ru/Operations/612752a2772ccc9fa7de6020
2021-08-26 11:36:52,157 INFO Collecting hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/spirit_data` (https://yql.yandex-team.ru/Operations/612752a2772ccc9fa7de6020)
2021-08-26 11:36:52,922 INFO YQL operation started: https://yql.yandex-team.ru/Operations/612752a4772ccc9fa7de6022
2021-08-26 11:36:54,145 INFO Collecting hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/balance_data` (https://yql.yandex-team.ru/Operations/612752a4772ccc9fa7de6022)
2021-08-26 11:36:54,914 INFO YQL operation started: https://yql.yandex-team.ru/Operations/612752a6772ccc9fa7de6027
2021-08-26 11:36:56,174 INFO Collecting hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/rnms` (https://yql.yandex-team.ru/Operations/612752a6772ccc9fa7de6027)
2021-08-26 11:37:02,202 INFO Pending hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/spirit_data`: RUNNING (https://yql.yandex-team.ru/Operations/612752a2772ccc9fa7de6020)
2021-08-26 11:37:04,173 INFO Pending hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/balance_data`: RUNNING (https://yql.yandex-team.ru/Operations/612752a4772ccc9fa7de6022)
2021-08-26 11:37:06,222 INFO Pending hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/rnms`: RUNNING (https://yql.yandex-team.ru/Operations/612752a6772ccc9fa7de6027)
...
2021-08-26 11:39:26,754 INFO Pending hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/rnms`: COMPLETED (https://yql.yandex-team.ru/Operations/612752a6772ccc9fa7de6027)
2021-08-26 11:39:26,754 INFO Collected hahn.`//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50/rnms` (https://yql.yandex-team.ru/Operations/612752a6772ccc9fa7de6027)
2021-08-26 11:39:28,852	INFO	Transfer task started: https://transfer-manager.yt.yandex-team.ru/task?id=d3be1759-58dc9afa-7486f0f6-b8b8274e&tab=details&backend=production
2021-08-26 11:39:28,852 INFO Collecting ofd-xdc.`//tmp/robot-match-receipts/execution_history/2021-08-26 11:36:50/rnms` (https://transfer-manager.yt.yandex-team.ru/task?id=d3be1759-58dc9afa-7486f0f6-b8b8274e&tab=details&backend=production)
...
```

## <a name="charts"></a>Графики
С дашборда можно перейти на редактирование конкретного графика ('...' на графике -> Редактировать).

Новый график можно создать по крайней мере двумя путями:
- дублировать существующий в режиме редактирования и сохранить его под новым именем,
- перейти на соответствующий "датасет" (слева вверху в режиме редактирования графика), и "создать чарт" со страницы датасета (справа вверху).

Сохранять лучше в те же папки где лежат другие графики (MatchReceiptStable/MatchReceiptUnstable) - автоматически прорастут нужные права на основании прав на папку.

Добавление графика/селектора на дашборд — через "редактировать" на странице дашборда.

### Алерты

* Данные для алертов собирает и отправляет в соломон [DBstats](https://a.yandex-team.ru/arcadia/payplatform/spirit/dbstats). 
* Соломон пересылает всё в Juggler, где автоматически генерируются агрегаты на каждый из алертов (см. [match_raw_events)](https://docs.yandex-team.ru/juggler/notifications/rules#match-raw-events)).
* [Все алерты сверки в Juggler](https://juggler.yandex-team.ru/aggregate_checks/?project=&query=project%3Dtrust_cashregisters%26(service%3Dunexpected*%7Cservice%3Dmissed*)&limit=80")
* [Правило нотификаций](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=62bd5122b65cc4548ffdd5cb&project=trust_cashregisters) создает тикет в очереди SPIRIT и назначает исполнителя по календарю дежурств.
* Что делать написано здесь: https://wiki.yandex-team.ru/spirit/alerts/#alertynasverku

## <a name="data"></a>Данные
В рабочей директории сверки есть две подпапки:
- `execution_history` - история запусков скрипта. Каждая из подпапок — все таблицы, порожденные одним из запусков сверки. Продовые графики на эти данные не смотрят, но их можно "опубликовать".
- `published` - данные для продовых графиков. По сути являются инкрементальным результатом множества сверок. Каждая из поддиректорий — одна из целевых таблиц. При запуске публикации данные за заданные дни перезаписываются.

## <a name="logic"></a>Логика
Процесс состоит из двух основных частей:
- расчёт данных сверки (команда match в скрипте),
- "публикация" данных (команда publish).

### Расчёт данных сверки
Запускаются YQL/TransferManager job-ы для вычисления указанных "целей" сверки и всех зависимостей этих целей.

Задать цели сверки можно через `--target_tables`, например:
```commandline
./match_receipts --start_date '2021-08-13' --end_date '2021-08-25' --yql_token "$(cat /path/to/yql_token)" --tm_token "$(cat /path/to/tm_token)" --default_base_yt_dir //tmp/some_path --hahn_base_yt_dir //home/balance/prod/spirit/receipts_matching/stable match --target_tables=trust
```

Сверка умеет досчитываться с произвольного места (скипает уже рассчитанные таблицы). Это, в частности, означает что при исправлении проблем в одном из запросов не обязательно пересчитывать всю сверку, достаточно убрать из рабочей папки все таблицы которые требуется пересчитать и перезапустить сверку.
Для запуска "досчитывания" сверки есть параметр `--run_datetime` туда нужно передать имя поддиректории `execution_history`. Если параметр не указан - в качестве имени поддиректории будет взято текущее время.


Для понимания общего плана вычислений может быть полезна команда `explain`. Она тоже принимает `--target_tables` и в ответ отдает PlantUml-скрипт для построения диаграммы с планом вычисления. Отрисовку PlantUML выполнять умеет, в частности, wiki.y-t.ru. [Примеры](https://wiki.yandex-team.ru/users/kirillovap/match/) планов выполнения.

Все таблицы посчитанные в процессе работы скрипта будут лежать на хане в папке вида `//home/balance/prod/spirit/receipts_matching/stable/execution_history/2021-08-26 11:36:50`. Это данные для истории, а не для графиков. Для того чтобы данные проросли на графики необходимо запустить их публикацию.
### Публикация
На данном шаге данные из указанной папки `execution_history/start_datetime` раскладываются по дням в `//home/balance/prod/spirit/receipts_matching/stable/published/...`. Публикуются все таблицы указанные как "публикуемые" в настройках скрипта (`script.py`), которые есть в этом папке.
При этом старые данные по дням со `start_date` до `end_date` полностью заменяются. На данные из `../published/...` натравлены все графики.
```commandline
./match_receipts --start_date '2021-08-13' --end_date '2021-08-25' --yql_token "$(cat /path/to/yql_token)" --tm_token "$(cat /path/to/tm_token)" --default_base_yt_dir //tmp/some_path --hahn_base_yt_dir //home/balance/prod/spirit/receipts_matching/stable publish
```

## Разработка

При внесении доработок могут помочь:
- Команды `explain`, `explain_query`.
- Запуск сверки локально без команды `publish` (только `match`) - для отладочного дашборда этого достаточно, а на продовые графики заведомо не повлияет.
- Можно явным образом задать директорию для результатов (`--run_datetime`): скрипт будет "досчитывать" те таблицы, которых нет в соответствующей папке и скипать остальные — удобно для отладки запросов.
- [Отладочный дашборд](https://datalens.yandex-team.ru/lg29jhvjo1q8e-sverki-kass-unstable). Графики могут разъезжаться с основным дашбордом, автоматической синхронизации пока нет. У этого дашборда свои источники данных, их можно, в частности, настроить на "неопубликованные" данные-результаты отладочного запуска.
- Тесты:
   - `./ut` - юнит-тесты, с подмоканными клиентами YQL и TransferManager.
   - `./it` - интеграционные тесты на behave с локальными yt+yql (поднимаются рецептом).

