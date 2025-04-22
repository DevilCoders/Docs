## Что это?
Из cooked-таблиц готовятся таблицы, которые используются для АБ-тестов и построения графиков в Даталенс
| Приложение | Cooked-таблицы | Метрики |
|------------|----------------|---------|
| Навигатор | [//home/maps/analytics/logs/cooked-metrika-mobile-log/navi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/navi) | [//home/maps/statistics/navi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics/navi) |
| МЯК | [//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps) | [//home/maps/statistics/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics/mobile-maps) |
| Таксометр | [//home/maps/analytics/logs/cooked-metrika-mobile-log/taximeter](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/taximeter) | [//home/maps/statistics/taximeter](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/statistics/taximeter) |

## Как запускается?
Код метрик запускается в Sandbox в задаче [MAPS_STATISTICS_METRICS](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsStatisticsMetrics)
от имени пользователя __robot-stats-navi__ в пуле __robot_stats_navi__.
Задачи создаются в шедьюлере и при каждом запуске проверяют, появились ли исходные таблицы. Если появились, то запускается расчет.

## "Дефолтная" схема вычислений
По умолчанию на вход подаются Cooked-таблицы, на выходе получаются таблицы со значениями метрик по поездкам:
| DrivingSessionID | Metric 1 | Metric 2 |
|------------------|----------|----------|
| id1 | m1_value1 | m2_value1 |
| id2 | m1_value2 | m2_value2 |

Cooked-таблицы отсортированы по полям ["DrivingSessionID", "EventTimestamp", "EventNumber"], то есть по сессиям, а внутри сессии - в хронологическом порядке.

Вычисление метрик по сессиям при таком формате исходных таблиц осуществляется операцией __Reduce__ по ключу "DrivingSessionID".

## Агрегаторы
Поскольку обычно требуется одновременно посчитать большое количество величин, то возникает необходимость разнесения кода для разных метрик по разным классам.

Для этого используются специальные классы-агрегаторы. Каждый такой класс описывает вычисление одной или нескольких величин. Примеры величин, которые можно посчитать агрегаторами:
 - сумма
 - максимум/минимум
 - было ли определённое событие в сессии
 - первое значение, встретившееся в определённом поле (например, строка, содержащая версию приложения)
 - объединение всех тестбакетов, которые встретились в поездке, в строку

Бывают и более сложные случаи, например, есть агрегаторы, в которых реализована стейт-машина

Список необходимых агрегаторов передаётся в конструкторе в специальный редьюсер [MetrikaReducer](https://a.yandex-team.ru/arc_vcs/maps/statistics/metrics/pylib/common/yt_operations.py), который обеспечивает параллельное выполнение всех агрегатов за один Reduce.

Также задачей агрегатора является описание типов возвращаемых значений. Из списка агрегаторов выводится схема итоговой таблицы.

Пример простейшего агрегатора, подсчитывающего количество событий в поездке. Базовый класс определён в [common/aggregators.py](https://a.yandex-team.ru/arc_vcs/maps/statistics/metrics/pylib/common/aggregators.py)
```python
class Count(Aggregator):
    def __init__(self, name):
        Aggregator.__init__(self, name, field_type="int64")
        self.count = 0

    def add(self, row):
        self.count += 1

    def result(self):
        return self.count
```

## Простейший пример кода метрики
Имея реализованный агрегатор, можно уже начать считать метрики. Простейший код будет выглядеть так:
```python
from common.yt_operations import MetrikaReducer, do_metrika_reduce
from common.log_reporter import LogAggregator
from common.utils import schema_v3
import datetime


class MyFirstAbt(LogAggregator):
    SUPPORTED_COMPONENTS = ["maps"]

    def __init__(self, cfg, period):
        LogAggregator.__init__(
            self,
            'my_first_abt',
            cfg,
            period,
            start_date=datetime.date(year=2022, month=2, day=1)
)

    def aggregate_logs(self, src_tables, dst_table, datestr, **kwargs):
        reducer = [
                Count()
            ])

        do_metrika_reduce(
            reducer,
            src_tables,
            dst_table,
            schema=schema_v3(reducer.agg_prototypes),
            reduce_by="DrivingSessionID",
            sort_by=("DrivingSessionID", "EventTimestamp", "EventNumber"),
            spec={"data_size_per_job": 2 * 1024 * 1024 * 1024}
        )
```
В этом примере будет посчитана метрика количества событий в поездке для приложения МЯК. Результатом работы станут таблицы в папке //home/maps/statistics/mobile-maps/production/aggregated_by_sessions/my_first_abt

## "Нестандартные" метрики
Иногда бывает необходимо посчитать метрику не на основе Cooked-таблицы, а на основе других таблиц. Или даже на основе одной таблицы, но с дополнительными данными из другой.
Базовый класс [LogReporter](https://a.yandex-team.ru/arc_vcs/maps/statistics/metrics/pylib/common/log_reporter.py) имеет возможности тонкой настройки для подобных случаев.
Смотри, например,

[Метрики ложных сходов](https://a.yandex-team.ru/arc_vcs/maps/statistics/metrics/pylib/false_route_lost.py), 

[Метрики покрытия альтернатив](https://a.yandex-team.ru/arc_vcs/maps/statistics/metrics/pylib/alternatives_coverage.py),

[Количество пользователей по типам](https://a.yandex-team.ru/arc_vcs/maps/statistics/metrics/pylib/user_type_log_abt.py)

## Добавление новой таблицы
Необходимо положить в директорию pylib файл с классом, унаследованным от common.log_reporter.LogAggregator.
При сборке этот класс будет автоматически подхвачен и доступен при запуске бинарника


## Тесты
### Описание
После того, как написан код, необходимо добавить тесты для всех новых отчетов.
Каждый тест состоит из конфига с описанием входных и выходных таблиц и папки с данными. .
Конфиги тестов лежат в Аркадии в папаке ARCADIA/maps/statistics/metrics/test_data/test_actors, данные - на Sandbox в виде ресурсов.

Конфиги имеют формат JSON и выглядят примерно так:
```
    {
        "component": "navigator", 
        "period": "Day", 
        "input": [
            {
                "table": "//home/logfeller/logs/navi-metrika-mobile-log/1d/2020-12-26", 
                "file": "input.yson",
                "schema": "input.schema"
            },
            {
                "table": "//home/logfeller/logs/appmetrica-location-log/1d/2020-12-26",
                "file": "location_input.yson",
                "sort_by": [
                 "AppID",
                 "ApiKey",
                 "DeviceID"
                ]
            }
        ], 
        "output": [
            {
                "table": "//home/statistics-navi/unittesting/event_log/garbage/2019-03-13", 
                "file": "garbage"
            }, 
            {
                "table": "//home/statistics-navi/unittesting/event_log/2019-03-13", 
                "file": "output"
            }
        ]
    }
```
Все семплы должны быть в формате YSON.
Для входных семплов настоятельно рекомендуется указать файл со схемой в описании входа (при условии, что таблица схематизирована).
Схема - файл с документом в формате YSON, для таблицы с путём //path/to/table схему можно получить командой
```
yt get --proxy hahn //path/to/table/@schema > input.schema
```
Сам семпл можно подготовить, например, при помощи YQL с последующим сохранением таблицы:
```
yt read --proxy hahn --format '<format=pretty>yson' //tmp/your_sample > input.yson
```
ВНИМАНИЕ: В схеме данных уже задан порядок сортировки таблицы. Поэтому файл input.yson должен быть уже отсортирован в соответствие со схемой,
иначе будет ошибка 'sort order violation' при загрузке семпла в локальный YT

Если у входной таблицы нет схемы, но таблица должна быть отсортирована по определённому ключу, то в описании входа можно указать параметр "sort_by" с указанием столбцов,
по которым необходимо отсортировать таблицу. В этом случае посли записи данных в локальный YT будет запущена операция сортировки по указанным ключам.

ВНИМАНИЕ: Одновременное указание схемы таблицы и параметра 'sort_by' не допускается.

При запуске тестов происходит следующее:
1. С Sandbox-а выкачиваются данные для всех тестов
2. Поднимается локальный YT
3. Для каждого актора ищется конфиг и в локальный YT в соответствии с конфигом загружаются исходные таблицы актора
4. В локальном YT запускается актор
5. Проверяется, совпадают ли выходные таблицы актора с эталонными таблицами.
  Если обнаружились расхождения - тест фейлится и таблица, получиваяся в результате запуска сбрасывается в папку tests/test_actors/test-results
6. Из YT удаляются таблицы и переходим к следующему актору

### Запуск тестов
Запуск тестов для всех акторов (очень долго):
```
    ya make -tA --test-stderr
```
Запуск тестов только для определённых акторов:
```
    ya make -tA --test-stderr --test-param actors=LogPreprocessor,GuidanceAbt
```
При разработке намного удобнее, когда тестовые данные лежат не на Sandbox, а локально. Путь к папке с тестами можно указать в параметре "test_root":
```
    ya make -tA --test-stderr --test-param actors=GuidanceReport,StandingReport --test-param test_root=path_to_my_test_root
```
В test_root все данные должны лежать в директориях, названных так же, как и акторы.
Если в test_root есть данные не для всех акторов, перечисленных в списке акторов (--test-param actors) - запуск завершится ошибко

### Добавление теста
1. Надо написать конфиг с описанием
2. Создать тестовые входные таблицы в формате json и поместить их в директорию test_root/NewActor
3. Запустить тест
```
    ya make -tA --test-stderr --test-param actors=NewActor --test-param test_root=path_to_my_test_root
```
4. Тест зафейлится, результат работы актора будет сброшен в tests/test_actors/test-results
5. Результат из tests/test_actors/test-results перенести в test_root/NewActor
6. Загрузить test_root/NewActor на Sandbox. Важно! не забыть указать бесконечный ttl:
```
    ya upload NewActor --ttl inf
```
7. Добавить ID ресурса в tests/test_actors/ya.make

## Релиз новой версии
После того, как код закоммичен в Аркадию, релиз делается так:
1. Надо в Sandbox запустить задачу типа
        MAPS_BUILD_STATISTICS_METRICS
После завершения работы все изменения будут подхвачены тестингом
2. Добыть Sandbox-токен
    https://sandbox.yandex-team.ru/oauth/token
3. Создаём шедьюлеры:
    ```
        create_schedulers/create_schedulers --token [YOUR_SANDBOX_TOKEN] --actor NewActor --action ALL --component ALL --period ALL --env ALL
    ```
    Любой параметр может иметь либо конкретное значение, либо ALL. После создания скриптом новые шедьюлеры надо запустить руками в Sandbox. Если шедьюлер с заданными параметрами уже существует, то скрипт его пропустит.
4. Когда решили, что все хорошо работает, жмём кнопку RELEASE у нашей таски MAPS_BUILD_STATISTICS_METRICS

## Изменение кода существующей метрики
Если требуется изменить уже существующую метрику без создания новой, то после изменения кода требуется
1. поправить тесты
2. в Sandbox запустить задачу типа
    MAPS_BUILD_STATISTICS_METRICS
3. Когда решили, что все хорошо работает, жмём кнопку RELEASE у нашей таски MAPS_BUILD_STATISTICS_METRICS
В шедьюлере менять ничего не надо

## Откат в случае обнаружения ошибки
Если все же что-то пошло не так, то надо заново запустить MAPS_BUILD_STATISTICS_METRICS, указав ревизию Аркадии, где все ещё было хорошо.
Таска отрабатывет, релизим, и, тем самым, откатываем сломанную версию из стейбла до рабочей

## Пересчёт уже существующих таблиц
Если вдруг в коде обнаружилась ошибка и некоторое количество таблиц посчиталось с ошибками, то пересчитать таблицы можно
1) Просто удалив ошибочные таблицы из YT. В этом случае они посчитаются автоматически.
2) Либо скомпилировав и запустив руками бинарник примерно следующей командой:
```
cd YOUR_ARCADIA/maps/statistics/metrics
ya make -r
ENV_TYPE=testing YT_TOKEN=`cat ~/.yt/token` bin/metrics --component maps --period Day --actor PedestrianRouteLostAbt --force-recalc-date 2022-02-08
```

