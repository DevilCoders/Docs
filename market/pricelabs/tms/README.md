# Описание проекта
Тяжелые фоновые процессы, выполняющие расчет стратегий, автостратегий (белых, синих, вендорских синих), загрузку всей необходимой статистики (как из mstat/PriceCenter, так и из YM/GA).

Основная концепция системы управления задачами описана отдельно: см. раздел _Управление задачами_ ниже.

Имеет ручки для выполнения служебных операций (см. [../api/README.md](../api/README.md)).
Основное описание интерфейсов: [internal-api.yaml](../core/src/main/resources/openapi/internal-api.yaml)

Ручки доступны как:
 * тестинг - [https://pricelabs-tms2.tst.vs.market.yandex.net](https://pricelabs-tms2.tst.vs.market.yandex.net)
 * прод - [https://pricelabs-tms2.vs.market.yandex.net](https://pricelabs-tms2.vs.market.yandex.net)


# Детали реализации

## Аутентификация в ручках (TVM2)
[../api/README.md](../api/README.md)

**clientId** в **API** и **TMS** одинаковые.


## Генерация ручек
[../api/README.md](../api/README.md)


## Работа с YT
И чтение, и запись выполняется через кластер реплицированных динтаблиц **markov**.

Для того, чтобы автоматически поддерживать структуру динтаблиц (привязывать их к бинам), у нас есть класс **ru.yandex.market.yt.DynamicTableInitializer**.
См. его использование в [ProcessingConfig](src/main/java/ru/yandex/market/pricelabs/tms/processing/ProcessingConfig.java).

Класс принимает описание таблиц (бины из [TmsTables](src/main/java/ru/yandex/market/pricelabs/tms/processing/TmsTables.java) и
[CoreTables](../core/src/main/java/ru/yandex/market/pricelabs/processing/CoreTables.java)) и создает для них таблиц как
на **markov**, так и на кластера динтаблиц **seneca-sas** и **seneca-vla**.

Такая генерация (в том числе и добавление столбцов, изменение некоторых параметров динтаблиц и т.д., и т.п.) выполняется при первом
запуске приложения с новой версией. Это означает что любое изменение динтаблиц должно быть обратно совместимым (можно только добавлять столбцы и
таблицы).

Для активного погружения в мир динтаблиц можно воспользоваться страницей https://wiki.yandex-team.ru/users/miroslav2/prakticheski-zametki-o-rabote-s-dintablicami-yt/


## Работа с PostgreSQL
Мы используем Liquibase как средство конфигурации DDL в БД PostgreSQL: [changelog.xml](src/liquibase/changelog.xml).
Обновление схемы Liquibase сделано отдельным этапом в наших пайплайнах.

PostgreSQL выступает как БД для хранения мета-информации - т.е. любых не business данных. А именно - там мы храним список задач на выполнение, логи этих задач, настройки экспорта, текущие версии таблиц и т.д.

См. [пакет services.database](src/main/java/ru/yandex/market/pricelabs/tms/services/database).


## Работа с MySQL
Мы все еще делаем запросы (и вставляем некоторые данные) в БД MySQL, интегрируясь с PLv1.

Настройки магазинов, фильтров, стратегий и пользователей лежат в MySQL PLv1, мы импортируем их в YT с помощью [AbstractSQLImportingProcessor.java и потомков](src/main/java/ru/yandex/market/pricelabs/tms/processing/imports/AbstractSQLImportingProcessor.java).

Запись: [PL1ExportProcessor.java](src/main/java/ru/yandex/market/pricelabs/tms/pl1/PL1ExportProcessor.java).


## Основная функциональность
 1. Расчет CPC стратегий для белого маркета для основании рекомендация через **ПАПИ/mbi-bidding**
 1. Управление скрытиями офферов через **ПАПИ**
 1. Подготовка CPC автостратегий для белого маркета через **АМУР**
 1. Подготовка CPC автостратегий для синего маркета через **АМУР**
 1. Подготовка CPC автостратегий для синих вендоров через **АМУР**
 1. Подготовка CPA автостратегий для DBS/белого маркета через **mbi-bidding**
 1. Отчеты по ценам конкурентов для **белого ПИ** и **PL**
 1. Аналитические отчеты для **PL** (ассортимент, заказы) с выгрузкой в CSV и Excel (в т.ч. фоновые в S3 для постоянного хранения)
 1. Ручки управления настройками автостратегий (синими, белыми, вендорскими) и вся необходимая обвязка для **белого ПИ**, **синего ПИ** и **вендорского ПИ**
 1. Источник вендорских рекомендаций по моделям для **вендорского ПИ**

### Обвязка
 1. Импорт всех необходимых данных для отчетов и стратегий из YT таблиц (**ПЦ**, **клики маркета**, **курсы валют** и т.д.)
 1. Импорт заказов из **GA/YM**
 1. Расчет таблиц со статистикой (по магазину, по офферам, по дню) для использования в аналитических отчетах и отображении в интерфейсе

## Управление задачами

### Quartz
Стандартный Scheduler задач с некоторыми маркетными улучшениями.
Используется **только** для периодических задач (т.е. выполняемых по расписанию, не чаще раза в минуту).

Как правило - это служебные задачи, выполняющую загрузку в PL данных из внешних источников, планирование новых циклов и т.д.

Все задачи описаны в [QuartzJobs.java](src/main/java/ru/yandex/market/pricelabs/tms/jobs/QuartzJobs.java).


### PL Jobs
Собственный движок управления задачами, рассчитанный на специфику PriceLabs.
 * Управляет всеми задачами конечного размера (всеми, которые требуется выполнить за конечное число попыток).
 * Оперирует группами tasks в рамках одной job
 * Поддерживает приоритеты
 * Умеет перезапускать упавшие задачи
 * Поддерживает запуск job в зависимости от успешного завершения предыдущей job
 * Имеет защиту от переполнения очереди задач (запрещает планировать новые job, если предыдущий такого же типа еще не завершился)
 * Оперирует от 20 000 до 100 000 активными task-ами в разных job-ах с latency порядка 20-60 миллисекунд (получение группы tasks для выполнения в процессе, с учетов всех приоритетов).

См. [TasksServiceImpl.java](src/main/java/ru/yandex/market/pricelabs/tms/services/database/TasksServiceImpl.java) и  [ядро управления задачами tms_start_tasks.sql](src/liquibase/init/functions/tms_start_tasks.sql) (именно это функция разбирает задачи для выполнения в нужном приоритете с учетом всех условий в конкурентном режиме).




## На что обратить внимание

### Источники офферов
Мы поддерживаем 2 источника офферов поколения Pricelabs (формируемых YQL операциями; скоро отомрет) и генлоги: таблицы, которые формирует индексаторы на основании поколения репорта (наиболее правильный источник данных).

У них разный формат и разная логика работы, соответствующие объекты имеют суффикс **Pl** и **Gen**.
Помимо офферов мы также загружаем и категории (скоро должна появиться и загрузка категорий из экспортного формата, привязанных к поколению).

### Репорт
Мы ходим в репорт за рекомендациями по офферам, моделям и списком конкурентов.
См. [пакет services.market_report](src/main/java/ru/yandex/market/pricelabs/tms/services/market_report).


### Индексатор
Сервис, которые позволяет определить, какое из поколений является активным (на каком кластере его искать).
См. [пакет services.market_indexer](src/main/java/ru/yandex/market/pricelabs/tms/services/market_indexer).


### Партнерское API (Partner-API/ПАПИ)
Загружаем текущие настройки магазина (перед началом обработки), некоторую статистику (дневные расходы), а также отправляем туда ставки (до полного перехода на mbi-bidding).
См. [пакет services.partner_api](src/main/java/ru/yandex/market/pricelabs/tms/services/partner_api).


### Amore (АМУР)
Сервис для настройки автостратегий, мы выгружаем туда информацию о текущих привязках АС к офферам (и настройки самих АС).
См. [пакет services.amore](src/main/java/ru/yandex/market/pricelabs/tms/services/amore).


### Яндекс.Метрика/Google Analytics
Доступ к YM/GA, откуда мы загружаем информацию о заказах (если магазин настроил такую загрузку в PL).
См. [пакет services.stats_orders](src/main/java/ru/yandex/market/pricelabs/tms/services/stats_orders).


### Цены закупки
Магазин может предоставить ресурс, откуда можно скачать "цены закупки".

Интегрируется с Самоваром, отправляя ему список ресурсов для загрузки "цен закупок" (позволяет эти цены хранить в наших таблицах и настраивать для них стратегии).

Формирование списка ресурсов для загрузки Самоваром: [PurchasePriceSourceExportProcessor.java](src/main/java/ru/yandex/market/pricelabs/tms/processing/offers/PurchasePriceSourceExportProcessor.java).

Чтение из скачанных Самоваром файлов: [PurchasePriceSourceImportProcessor.java](src/main/java/ru/yandex/market/pricelabs/tms/processing/offers/PurchasePriceSourceImportProcessor.java).


## Генерация проекта IDEA
Можно запустить как: `ya ide idea market/pricelabs`

А можно и чуть поинтереснее, взяв специальный пускатель [ya-idea](../../../direct/bin/ya-idea):
```
cd market/pricelabs
ya-idea
```

## Запуск тестов

### Запуск тестов из командной строки
Только small + проверка стилей (рекомендуется перед PR):
```
ya make -t
```

Все тесты PLv2 (только на Linux):
```
ya make -tt
```

### Запуск тестов на distbuild с локальным YT (Mac)
YT работает только под Linux-ом, но если хочется проверить его работу в локальном режиме на Mac,
то запускать тесты нужно в режиме распределенной сборки:
```
ya make -tt --target-platform=linux --dist --yt-store
```
**Note:** Опция `-E` скачает все результаты сборки (включая логи).

**Note:** Именно так будут выполняться тесты при создании PR, поэтому локально запускать это, как правило, не нужно.



### Запуск тестов из IDEA
Всегда полезно добавить:
```
-Djava.awt.headless=true
```

Запускайте с переменной окружения, если находитесь не в московской временной зоне:
```
-Duser.timezone=Europe/Moscow
```

#### Выдача прав (если не используется локальный YT, см. ниже)
Потребуются права на **read/write/remove + mount**
[в каталогом `//home/market/development/pricelabs` на Zeno](https://yt.yandex-team.ru/zeno/navigation?path=//home/market/development/pricelabs),
а также нужно добавить пользователя в группу `pricelabs`, которая  может использовать наш аккаунт: [пример](https://idm.yandex-team.ru/system/yt-cluster-zeno#role=15973230,f-role-id=15973230).

Для подключения к кластеру ваш персональный токен YT должен лежать в файле `~/.yt/token`

#### Запуск с локальным PostgreSQL в докере
Запускаете PostgreSQL в докере единожды, пробросив порт:
```
docker run --name pricelabs_postgresql -e POSTGRES_PASSWORD=postgres -dp 15432:5432 postgres:10
```

Задаете переменную окружения для всех тестов:
```
PG_LOCAL_PORT=15432
```

Запускаете тесты: при каждом запуске будет подготовлена своя схема с уникальным именем.


#### Запуск с локальным YT в докере

Запускаете YT в докере, пробросив порт (без паролей и доп. настроек), как описано в https://github.yandex-team.ru/yt/docker

Задаете переменную окружения для всех тестов:
```
YT_PROXY=localhost:8000
```

Запускаете тесты: при каждом запуске будет подготовлен свой каталог с уникальным именем.

**Note:** YT в докере потребляет много CPU. При ограничении в одно ядро (Docker) он расходует от 50% в простое
до 100% одного ядра во время работы тестов.

**Note:** В таком режиме не работают YQL тесты.

#### Запуск с YT и PostgreSQL на виртуальной машине
Существует вариант поднять и YT, и PostgreSQL на виртуальной машине в облаке QYP.

Это хороший компромисс между локальностью и эффективностью. Тесты работают значительно быстрее, чем в облачном PosgreSQL и YT, но мы не тратим память и CPU на Докер и YT - это может быть важно при работе на Mac, где докер представляет собой обычную виртуальную машину и потребляет очень много ресурсов.

Нужно завести себе машину в QYP: https://qyp.yandex-team.ru/

**YT**:
1. Подготавливаем YT: https://yt.yandex-team.ru/docs/other/local_mode
1. Запускаем: ```miroslav2@miroslav2-build:~/yt$ yt_local start --id miroslav2 --proxy-port 12001 --rpc-proxy-count 1```
1. Прописываем в шаблонах Unit тестов: `YT_PROXY=miroslav2-build.vla.yp-c.yandex.net:12001`

**PostgreSQ**:
1. Подготавливаем PG: `sudo apt install postgresql-10`
1. Открываем доступ в файле `/etc/postgresql/10/main`:  `host  all  all all md5`
1. Задаем пароль: https://stackoverflow.com/questions/12720967/postgresql-how-to-change-postgresql-user-password (`postgres:postgres` сейчас ожидаются по умолчанию)
1. Прописываем в шаблонах Unit тестов:
```
PG_LOCAL_HOST=miroslav2-build.vla.yp-c.yandex.net
PG_LOCAL_PORT=5432
```

**Note:** В таком режиме не работают YQL тесты.

#### Переиспользование схемы YT и PostgreSQL
Чтобы запускать тесты значительно быстрее (не тратя до 30 секунд на инициализацию схемы PostgreSQL и таблиц YT),
можно передать во все тесты переменную окружения
```
REUSE_INSTANCE=10500
```
Это начало диапазона портов (10500..10509 в нашем примере). Диапазон используется для гарантии уникального идентификатора
схем при запуске нескольких тестов одновременно (если порт занят, то к названию схемы YT или PostgreSQL прибавляется единица).

**Внимание:** если в схему YT или PostgreSQL вносятся несовместимые изменения, то проще всего будет полностью очистить
каталог с таблицами YT или схему PostgreSQL (либо просто пересоздать docker контейнер).

### Периодическая очистка каталога с тестами (если не используется локальный YT)
Все еще не автоматизировано - нужно заходить и чистить каталог
[на кластере Zeno: `//home/market/development/pricelabs/unit-tests`](https://yt.yandex-team.ru/zeno/navigation?path=//home/market/development/pricelabs/unit-tests)



## Запуск приложения локально

### Запуск

Класс для запуска: `ru.yandex.market.pricelabs.tms.Main`

VM Options:
```
-Denvironment=testing
-Dspring.profiles.active=development
-Dserver.port=8081
-Dconfigs.path=${ARC}/market/pricelabs/tms/src/main/properties.d
-Dlocal.properties=${HOME}/secret/tms/testing/secrets.properties
-Dlogging.config=${ARC}/market/pricelabs/tms/src/test-medium/resources/log4j2-test.xml
-Dpricelabs.juggler.url=http://juggler-push.search.yandex.net
-Dserver.max-http-header-size=64000
-Dpricelabs.main.jdbc.maxConnections=2
-Dpricelabs.target.yt.table.retryCount=3
-Xmx1g
```


 * `${ARC}` - смотрит на корень примонтированного arc репозитория
 * `${HOME}/arc/.build` - каталог для сборки (`output_root = "${YA_ARCADIA_ROOT}/../.build"`)
 * [Файл секретов `${HOME}/secret/tms/testing/secrets.properties`](https://yav.yandex-team.ru/secret/sec-01dd1506mk45zmz2cyt3rs8a3x/explore/versions)

Приложение поднимется по адресу http://localhost:8081
