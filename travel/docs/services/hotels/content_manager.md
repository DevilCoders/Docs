---
title: Контент-платформа
---

# Content manager

Терминология:
* Управляющий контур – периодически запускаемый процесс, который выполняет триггеры и апдейтеры, и поддерживает структуру хранилища.
* Хранилище – набор табличек в YT, хранящие текущие данные контентного менеджера
* Сущность хранилища – пермалинк / пермарум / маппинг (он же оффер)
* Стадия – кусочек общего контентного Workflow. Состоит из триггера, процессора и апдейтера.
* Триггер – код управляющего контура, анализирующий необходимость запуска процессора, и подготавливающий для него входные данные. Выполняется в управляющем контуре.
* Процессор – код, выполняющий какую-либо операцию над данными. Запускается в виде отдельного графа в нирване.
* Апдейтер – код управляющего контура, обрабатывающий результаты выполнения процессора – вносит изменения в хранилище. Выполняется в управляющем контуре.
* Диспетчер – код управляющего контура, определяющий последовательность выполнения стадий для каждой сущности

## Взаимосвязь стадий

У каждой сущности хранилища для каждой стадии, на которую она может быть передана, есть флажок, принимающий одно из трех состояний:
* Сущность не нуждается в обработке на данной стадии
* Сущность нуждается в обработке на данной стадии
* Сущность уже обрабатывается на данной стадии

Триггер стадии сканирует все сущности интересного ему типа в поисках тех, которые нужно обработать на данной стадии и проставляет им флаг "уже обрабатывается", и складывает данные сущности во входную таблицу процессора. Кроме того, триггер может регулировать поток данных в процессор: например, можно наложить ограничение на размер задания в янге/толоке: минимальный (чтобы не запускать задания на разметку одного маппинга) и/или максимальный (не размечать за раз более 5000 маппингов, т.к. результат нужно будет ждать слишком долго).

Далее запускается процессор, и формирует выходную таблицу.

Затем запускается апдейтер (в рамках управляющего контура), обрабатывает выходную таблицу процессора, обновляя хранилище:
* для текущей стадии проставляет флаг "не нуждается в обработке"
* для каких-то других стадий, которые зависят от текущей, проставляет флажок "нуждается в обработке" (можно с произвольным условием, например "только 5%").

Данный подход позволяет строить произвольные взаимосвязи между стадиями.

## Диспетчеризация

Отвечает за последовательность выполнения стадий для каждой сущности. Диспетчеризация работает поверх логики, описанной в разделе "Взаимосвязь стадий"

При запуске процесса обработки указывается список стадий `required_stages`, которые обязательно должна пройти сущность. Если сущность успешно обработана на всех стадиях или на одной из стадий произошла ошибка, сущность отправляется на завершающую стадию

Для каждой стадии можно указать список стадий, которые должны быть выполнены до указанной стадии `{stage}_required_stages`

Комбинация `required_stages` и `{stage}_required_stages` позволяют задать произвольный граф выполнения стадий. Граф может дополняться во время обработки сущности

Зацикливание в графе не допускается

## Процессоры: python vs произвольный граф в нирване

С точки зрения управляющего контура, любой процессор – это просто какой-то внешний процесс, который потребляет входные таблицы, и генерирует выходные. Есть два типичных варианта написания процессоров:
1. Код на python. Применяется, если процессор лаконично выражается на python. Запускается в виде специального графа в нирване, который запускает python-executable.
2. Произвольный граф. Применяется, если уже есть готовый граф для какого-то контентного процесса, например, работа с асессорами/толокерами.

В целом, вариант "код на python" является предпочтительным, т.к. позволяет хранить код контент платформы в одном месте, версионировать и обновлять стандартным образом.

Процессор не должен сохранять какое-либо состояние, процессор должен выполнятся полностью детерминистически от входа и внешних read-only данных навроде логов сёрчера и офферкэша.

## Мотивация подхода

Вышеописанный подход сделан таким чтобы:
1. зафиксировать четкую структуру хранилища (описывается в виде python dataclass) и обеспечить его миграцию.
2. зафиксировать четкий интерфейс запуска каждого процессора (описывается в виде python dataclass).
3. предоставить возможность добавления стадий с минимизацией риска разрушения всего контент-процесса (за счет структуры хранилища и стандартизованного подхода к описанию стадии).
4. предоставить стандартные механизмы для версионирования и ревью кода контент-платформы.

## Описание стадий в коде

Все стадии находятся в папке [stages](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/stages/). Каждая стадия – отдельная папка внутри stages. Названия файлов для каждого из компонентов приведены далее. Общий код стадий находятся в папке [stages_common](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/stages_common/).

### Триггер

Файл: `trigger.py`

Триггер обрабатывает следующие события:
* **Сущности направлены на обработку в текущую стадию**.
Триггер получает из хранилища сущности, направленные на обработку в текущей стадии, а также, необходимые связанные сущности. Полученные данные преобразуются к формату, согласованному с процессором
* **Обработка ручных запросов**.
В этом случае триггер передаёт на вход процессора данные из папки `//home/travel/prod_inbox/content_manager/{stage_name}/{job_id}` или `//home/travel/testing_inbox/content_manager/{stage_name}/{job_id}`. `job_id` должен быть уникальным
* **Отслеживание изменений в хранилище**
Срабатывает, если в хранилище произошли какие-либо изменения

Триггер позволяет задавать разные наборы параметров обработки сущностей при подготовке задания для процессора (например, id пула для толоки или интервал времени для отложенной обработки сущности). Сущности, соответствующие определённому набору параметров выбираются с помощью фильтров. Набор фильтров для стадии – словарь, в котором ключ – название фильтра, значение – фильтрующая функция `ThreadFilter`. Название фильтра также является ключом для набора параметров. По-умолчанию создаётся фильтр `default`, который позволяет применять один набор параметров для всех сущностей

Подготовка задания для процессора выполняется в методе `prepare_data` класса `Producer`. На вход передаются отфильтрованные сущности и набор параметров, соответствующих фильтру

Общая логика работы триггера реализована в [lib/trigger.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/lib/trigger.py)

### Процессор

Файл: `processor.py`

Для тех случаев, когда процессор реализуется на python. Общие компоненты:
* [lib/processor.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/lib/processor.py)
* [processors_exec](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/processors_exec/)

### Мок

Файл: `mock.py`

Используется в специальном тестовом окружении. Замена процессора для тех случаев, когда:
* работа процессора подразумевает ручные действия (задания в толке или янге)
* процессор работает очень долго

### Апдейтер

Файл: `updater.py`

Общая логика работы апдейтера реализована в [lib/updater.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/lib/updater.py)

## Persistence manager

Persistence manager ([lib/persistence_manager.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/lib/persistence_manager.py)) – абстракция для различных способов хранения данных. Основные типы операций:

* преобразование имён/путей
* копирование/перемещение/удаление
* чтение/запись
* `select`/`upsert`
* транзакции

### `select`/`upsert`

Эти операции позволяют считать/записать подмножество данных хранилища, необходимых для работы. Используются в триггерах и апдейтерах для обработки сущностей, используемых на соответствующей стадии

### Реализации Persistence manager:

* **LocalPersistenceManager** – хранит данные в локальной ФС. Дерево каталогов/таблиц YT отображается на дерево каталогов/файлов локальной ФС. Данные хранятся в файлах, где каждая строка – строка таблицы, сеарилизованная в *JSON*. `select`/`upsert` реализованы на *Python*
* **YtPersistenceManager** – хранит данные в *YT*. `select`/`upsert` выполняют *YQL*, сгенерированный по заданным параметрам

## Хранилище

Структура хранилища описана в [data_model/storage.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/data_model/storage.py)

### Организация хранилища

* каждая таблица описывается в виде dataclass
* для всех полей обязательно указывать тип и значение по-умолчанию
* поля, входящие в ключ задаются в `metadata['is_key']`, набор значений полей ключа уникален для таблицы
* связи между таблицами указываются через `metadata['foreign_key']`

### Снэпшоты хранилища

Управляющий контур сохраняет копию хранилища при изменении (снэпшот). Это гарантирует консистентность и неизменяемость снэпшота. Актуальный снэпшот доступен по симлинку `storage` в корневом каталоге проекта. Если процессору нужно работать с хранилищем, единственный правильный способ – добавить во входную папку хранилища symlink на снэпшот. Для этого в [триггере](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/lib/trigger.py) теперь есть метод `add_storage_link`. Процессор получает доступ к хранилищу по `{root}/stages/{stage_name}/input/{job_id}/storage`, а не `{root}/storage`. Пути к таблицам хранилища можно получить из [lib/path_info.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/lib/path_info.py). Для триггера и апдейтера `storage_path` указывает на `{root}/storage`, а для процессоров – на `{root}/stages/{stage_name}/input/{job_id}/storage`

### Программный интерфейс

Программный интерфейс хранилища ([lib/storage.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/lib/storage.py)) позволяет работать с хранилищем в виде иерархии сущностей **Пермалинк** == **URL** -> **Пермарум** -> **Маппинг**. Так к пермалинку можно добавить пермарумы и неразмеченные маппинги, к пермаруму – соответствующие маппинги, ...

## Миграция хранилища

Миграция выполняется автоматически при каждом запуске управляющего контура по описанию [хранилища](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/data_model/) и [версий хранилища](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/migrations/).  Для этого последовательно сравниваются все `storage_{n}.py` с `n` больше, чем версия хранилища, их разница применяется к хранилищу

Как мигрировать:
* скопировать `storage.py` в `storage_{n}.py`, `n = max(n) + 1`
* внести необходимые изменения в `storage.py`

Миграция выполняется при каждом запуске [управляющего контура](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/exec/), т.о. задачи управляющего контура всегда работают с последней версией хранилища

### Дополнительные миграции

Если во время миграции нужно вычислить новые поля по данным из существующих, можно использовать [дополнительные миграции](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/migrations/additional_migrations.py). Дополнительная миграция – произвольный код, который выполняется после основной миграции соответствующей версии. Привязка к версии задаётся в `ADDITIONAL_MIGRATIONS`

## Настройки

Настройки задаются в привязке к окружению. Формат описывается в [data_model/options.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/data_model/options.py). Окружение, описанное в [exec/options](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/exec/options/) в виде ресурсов, выбирается аргументом командной строки `--env`. Для development конфигураций настройки можно брать из локального файла (`--env-fn`).

## Процессы

### Вайтлистинг (clusterization, actualization)

Для запуска процесса нужно положить таблицу с пермалинками по одному из путей
* `//home/travel/testing_inbox/content_manager/wl_start/{job_id}/permalinks`
* `//home/travel/prod_inbox/content_manager/wl_start/{job_id}/permalinks`

Через 15-30 минут данные таблицы будут приняты в обработку, а сама таблица будет удалена

При создании таблицы из Нирваны в параметрах блока записи таблицы нужно выбрать режим "Создание таблицы". Имя выходной таблицы задавать выражением, в котором вместо `job_id` указать `${meta.operation_uid}`

Выбор значения из входной таблицы:

Ситуация                                     | Способ объединения
---------------------------------------------|--------------------
пермалинка нет в хранилище                   | замена
пермалинк в хранилище, но не обрабатывается  | замена
пермалинк в хранилище, в обработке           | слияние

* Замена – берётся значение, указанное во входной таблице
* Слияние – зависит от дополнительных параметров:
  * если указан тип `item_type`, в выходное значение запишется результат объединения (дополнения) множеств значений
  * если указана функция `merger`, в выходное значение запишется результат выполнения этой функции

[Формат таблицы](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/content_manager/data_model/stage.py) в классе `WLStartData`. Для описания используются такие правила:
* поля с типом Optional не обязательны, все остальные – обязательные
* если указан тип `item_type`, поле – строка со значениями из `item_type`, разделёнными запятой (пробелы не допускаются)
* `value` – значение, которое будет использоваться для поля, если не задано во входной таблице
* `replace` – всегда использовать для поля режим замены
* `merger` – функция, которая будет применяться для объединения значений

Возможные сценарии запуска:
* **актуализация** -> **кластеризация**
```
required_stages = "clusterization"
clusterization_required_stages = "actualization"
```
* **кластеризация**
```
required_stages = "clusterization"
```
* **актуализация**
```
required_stages = "actualization"
```

**Особый приоритет** `0x7fffffffffffffff` позволяет отправлять на обработку пермалинки до окончания уже запущенных заданий

Ссылки:
* Проект в Толоке/Янге [тестинг](https://sandbox.toloka.yandex.ru/requester/project/20332) [прод](https://yang.yandex-team.ru/requester/project/6074)
* Процесс в Хитмане [тестинг](https://hitman.yandex-team.ru/projects/travel_content_manager_catroom/cm-clusterization-basic-test) [прод](https://hitman.yandex-team.ru/projects/travel-content-manager-catroom-prod/cm-clusterization-prod)
* Дашборд в Соломоне [тестинг](https://solomon.yandex-team.ru/?project=travel&cluster=push_testing&service=content_catroom&dashboard=content-whitelisting) [прод](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=content_catroom&dashboard=content-whitelisting)
* История выполнений [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/content_manager/catroom/history/clusterization) [прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/content_manager/catroom/history/clusterization)

Рецепты:

Проверка статуса вайтлистинга
```sql
USE hahn;

$split_to_set = ($text) -> (
    ToSet(ListFilter(
        String::SplitToList($text, ","),
        ($x) -> ($x != "")
    ))
);

-- проверяет, что процесс вайтлистинга когда-либо запускался
$is_wl_started = ($required_stages) -> (
    $required_stages != ""
);

-- проверяет, что процесс вайтлистинга завершён
$is_wl_finished = ($required_stages, $finished_stages, $status_wl_clusterized_hotels) -> (
    $is_wl_started($required_stages) AND
    DictLength(SetDifference(
        $split_to_set($required_stages),
        $split_to_set($finished_stages),
    )) == 0 AND
    $status_wl_clusterized_hotels == "nothing_to_do"
);

-- статус обработки для всех пермалинков
SELECT
    p.*,
    $is_wl_started(p.required_stages) AS is_wl_started,
    $is_wl_finished(p.required_stages, p.finished_stages, p.status_wl_clusterized_hotels) AS is_wl_finished,
FROM `home/travel/prod/content_manager/catroom/storage/permalinks_wl` AS p;

-- пермалинки из задания, для которых обработка ещё не завершена
SELECT
    p.*,
FROM `home/travel/prod/content_manager/catroom/history/wl_start/ea1bdfc5-2977-4378-b05e-a5de56f8d857/input/permalinks` AS job
LEFT JOIN `home/travel/prod/content_manager/catroom/storage/permalinks_wl` AS p
USING (permalink)
WHERE NOT $is_wl_finished(p.required_stages, p.finished_stages, p.status_wl_clusterized_hotels);

```

### Проверка провязок толокерами (wl_match_hotels)

#### Запуск процесса

Для запуска процесса нужно положить таблицу с пермалинками по одному из путей
* `//home/travel/testing_inbox/content_manager/wl_new_hotels/{job_id}/permalinks`
* `//home/travel/prod_inbox/content_manager/wl_new_hotels/{job_id}/permalinks`

Через 15-30 минут данные таблицы будут приняты в обработку, а сама таблица будет удалена

При создании таблицы из Нирваны в параметрах блока записи таблицы нужно выбрать режим "Создание таблицы". Имя выходной таблицы задавать выражением, в котором вместо `job_id` указать `${meta.operation_uid}`

#### Формат таблицы

```
    permalink: uint                     # пермалинк
    grouping_key: str                   # ключ группировки (пермалинки с разными ключами не обрабатываются в одном пуле)
                                        # здесь можно указать название региона, номер тикета, ...
                                        # grouping_key пробрасывается в название пула
```

Схема для YT

```
[
  {"name": "permalink", "type": "uint64", "required": true},
  {"name": "grouping_key", "type": "string", "required": true}
]
```

Ссылки:
* Проект в Толоке/Янге [тестинг](https://sandbox.toloka.yandex.ru/requester/project/24840) [прод](https://toloka.yandex.ru/requester/project/32146)
* Процесс в Хитмане [тестинг](https://hitman.yandex-team.ru/projects/travel_content_manager_catroom/wl-match-hotels-test) [прод](https://hitman.yandex-team.ru/projects/travel-content-manager-catroom-prod/wl-match-hotels-prod)
* Дашборд в Соломоне [тестинг](https://solomon.yandex-team.ru/?project=travel&cluster=push_testing&service=content_catroom&dashboard=content-whitelisting) [прод](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=content_catroom&dashboard=content-whitelisting)
* История выполнений [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/content_manager/catroom/history/wl_match_hotels) [прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/content_manager/catroom/history/wl_match_hotels)

### Актуализация описаний классов обслуживания (sc_update_descriptions)

#### Форматы данных

Для актуализации описаний используются данные, полученные процессами, запускаемыми вне КП

* Перевозчики [//home/travel/prod/train/service_classes/carriers](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/train/service_classes/carriers&)

```
    carrier_code: str   # код перевозчика
    carrier_name: str   # название перевозчика
    country: str        # страна
    url: str            # сайт перевозчика
    enabled: bool       # нужно ли обновлять данные для этого перевозчика
```

* Типы вагонов [//home/travel/prod/train/service_classes/car_types](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/train/service_classes/car_types&)

```
    car_type_code: str  # код типа вагона
    car_type_name: str  # название типа вагона
    enabled: bool       # нужно ли обновлять данные для этого типа вагона

```

* Классы обслуживания [//home/travel/prod/train/service_classes/service_classes](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/train/service_classes/service_classes&)

```
    carrier_code: str   # код перевозчика
    car_type_code: str  # код типа вагона
    sc_code: str        # код класса обслуживания
    sc_name: str        # название класса обслуживания
```

#### Запуск процесса

Для запуска процесса нужно положить таблицу с классами обслуживания по одному из путей
* `//home/travel/testing_inbox/content_manager/sc_new_descriptions/{job_id}/descriptions`
* `//home/travel/prod_inbox/content_manager/sc_new_descriptions/{job_id}/descriptions`

Через 15-30 минут данные таблицы будут приняты в обработку, а сама таблица будет удалена

При создании таблицы из Нирваны в параметрах блока записи таблицы нужно выбрать режим "Создание таблицы". Имя выходной таблицы задавать выражением, в котором вместо `job_id` указать `${meta.operation_uid}`

Формат таблицы:
```
    carrier_code: str     # код перевозчика
    car_type_code: str    # код типа вагона
    sc_code: str          # код класса обслуживания
```

ВАЖНО!!! Запускать на обработку нужно только те классы обслуживания, для которых разрешены перевозчик и тип вагона (`enabled == True` в соответствующих таблицах)

Пример запроса для запуска процесса в тестинге:
```sql
PRAGMA yt.InferSchema = “20”;

USE hahn;

INSERT INTO `home/travel/testing_inbox/content_manager/sc_new_descriptions/descriptions` WITH TRUNCATE
SELECT DISTINCT
    sc.carrier_code AS carrier_code,
    sc.car_type_code AS car_type_code,
    sc.sc_code AS sc_code,
FROM `home/travel/prod/train/service_classes/service_classes` AS sc
LEFT JOIN `home/travel/prod/train/service_classes/carriers` AS carriers
ON sc.carrier_code == carriers.carrier_code
LEFT JOIN `home/travel/prod/train/service_classes/car_types` AS car_types
ON sc.car_type_code == car_types.car_type_code
WHERE carriers.enabled AND car_types.enabled
```

#### Экспорт результатов

Результаты обновления описаний выгружаются в таблицы:
* [тестинг] [//home/travel/testing/train/service_classes/descriptions](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/train/service_classes/descriptions&)
* [прод] [//home/travel/prod/train/service_classes/descriptions](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/train/service_classes/descriptions&)

```
    carrier_code: str             # код перевозчика
    car_type_code: str            # код типа вагона
    sc_code: str                  # код класса обслуживания
    data_source: str              # сайт, с кокторого получено описание
    sc_description: str           # описание класса обслуживания
    sc_description_original: str  # исходное описание класса обслуживания (как получено с сайта)
    sc_description_specific: str  # особое описание для отдельных номеров поездов
```

#### Ссылки:
* Проект в Толоке/Янге [тестинг](https://sandbox.toloka.yandex.ru/requester/project/33414) [прод](https://yang.yandex-team.ru/requester/project/6747)
* Процесс в Хитмане [тестинг](https://hitman.yandex-team.ru/projects/travel_content_manager_catroom/cm-sc-update-descriptions-test) [прод](https://hitman.yandex-team.ru/projects/travel-content-manager-catroom-prod/cm-sc-update-descriptions-prod)
* Дашборд в Соломоне [тестинг](https://solomon.yandex-team.ru/?project=travel&cluster=push_testing&service=content_catroom&dashboard=content-service-class) [прод](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=content_catroom&dashboard=content-service-class)
* История выполнений [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/content_manager/catroom/history/sc_update_descriptions&) [прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/content_manager/catroom/history/sc_update_descriptions&)
