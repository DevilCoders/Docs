## Что это?
Препроцессор логов готовит таблицы статистики из таблиц с событиями метрики и таблиц с локейшенами.
На выходе данные выводятся в удобном для дальнейших вычислений формате.

| Приложение | Исходные таблицы | Cooked-таблицы | Cooked-таблицы (тестинг) |
|------------|------------------|----------------|--------------------------|
| Навигатор | [//home/logfeller/logs/navi-metrika-mobile-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/navi-metrika-mobile-log/1d)<br><br>[//home/logfeller/logs/appmetrica-location-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-location-log/1d) | [//home/maps/analytics/logs/cooked-metrika-mobile-log/navi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/navi) | [//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/navi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/navi) |
| МЯК | [//home/logfeller/logs/appmetrica-yandex-events/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-yandex-events/1d)<br><br>[//home/logfeller/logs/appmetrica-location-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-location-log/1d) | [//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/mobile-maps) | [//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/mobile-maps](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/mobile-maps) | 
| Таксометр | [//home/logfeller/logs/taxi-metrika-mobile-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi-metrika-mobile-log/1d)<br><br>[//home/logfeller/logs/appmetrica-location-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/appmetrica-location-log/1d) | [//home/maps/analytics/logs/cooked-metrika-mobile-log/taximeter](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log/taximeter) | [//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/taximeter](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs/cooked-metrika-mobile-log.6p/taximeter) | 

## Препроцессинг
Основные действия, которые делает препроцессор:
1) Фильтрация нужных полей из исходных таблиц
2) Фильтрация нужных типов событий
3) Джойн таблиц с событиями с таблицей с локейшенами
4) Конвертация текстовых полей в числовые
5) Выделение DrivingSession и определение типа ведения
6) Выделение UserSession
7) Присвоение экспериментов (TestBuckets)
8) Сортировка таблицы по ["DrivingSessionID", "EventTimestamp", "EventNumber"]

### Разбиение на поездки (DrivingSession)
Основной единицей для вычисления статистики является полездка (DrivingSession). 

Поездка - это попытка формализовать понятие "Поездка из точки А в точку Б"
Каждому событию присваивается ID поездки, при этом есть условия, при которых начинается новая поездка:
1) Пользователь финишировал
2) Произошёл таймаут
3) Пользователь построил новый маршрут, конечная цель которого находится на значительном расстоянии от предыдущей конечной точки
4) Пользователь сменил тип ведения

При установке маршрута определяется тип ведения (авто, пешеходное и т.д.) и всем событиям до сброса маршрута или до финиша проставляется соответствующий  VEHICLE_TYPE

### Разбиение на пользовательские (UserSession)
Для подсчёта аудиторных метрик событиям присваиваются так называемые пользовательские сессии. 

Сейчас пользовательские сессии определяются следующим образом: 
1) По умолчанию пользовательская сессия не проставляется (= None)
2) При появлении события из списка активных событий мы считаем, что началось активное взаимодействие с приложением и начимнаем пользовательскую сессию
3) Если по прошествии определённого времени не было событий из списка активных, то считаем, что активное взаимодействие с приложением закончилось и пользовательскую сессию закрываем

### Тестбакеты
Для того, чтобы можно было проводить А/Б эксперименты, необходимо уметь вычислять значения метрик для разных выборок.
Когда мапкит получает конфиг экспериментов, то в АппМетрику логируетсф событие "get-experiments-info", в котором содержится вся информация об экспериментах, в которых участвует пользователь.
При получении данного события из него извлекаются номера выборок и номера соответствующих выборкам тестбакетов, которые добавляются в поле TestBuckets во все последующие события.

## Тестинг
Для целей проверки и отладки кода сделано специальное окружение - тестинг. Тестовый препроцессор на вход получает те же таблицы,  но делается дополнительный map, в котором остаются только UUID, начинающиеся с символа 'a'. Таким образом, объём тестовых данных в 16 раз меньше.
Тестовые таблицы кладутся в директории, оканчивающиеся на ".6p" (~6%)

## Обработка ошибок

В исходных таблицах время от времени попадаются невалидные данные. Для понимания того, что происходит, ошибки обрабатываются и строки, вызвавшие исключения, складываются в таблицы в папке garbage, которая находится в папке с cooked-таблицами. Текст ошибки записывается в специальное поле "what"

## Как запускается?
За запуск препроцессора отвечает Reactor. Условием запуска является готовность артефактов входных таблиц.
Реакции и артефакты Реактора конфигурируются системой Лама, конфиги лежат здесь: [тестинг](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/logs/cooked-metrika-mobile-log.6p)
[продакшен](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/logs/cooked-metrika-mobile-log)

Код препроцессора запускается в Sandbox в задаче [MAPS_STATISTICS_LOG_PREPROCESSOR_V_2](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsStatisticsLogPreprocessorV2)
от омени пользователя __robot-maps-analytics__ в пуле __maps-analytics-priviliged__

## Как перезапускать?
Если в коде обнаружилась ошибка, требуется пересчитать уже существующие таблицы. Так как препроцессор запускается через Reactor, то перезапуск следует (чтобы актуализировать соответствующие артефакты) через клонирование реакции:

![Перезапуск реакции](./docs/img/reactor.png)


## Тесты
### Описание
После того, как внесены изменения в код, необходимо поправить тесты.
Тест состоит из конфига с описанием входных и выходных таблиц и папки с данными. .
Конфиги лежат в Аркадии в папке ARCADIA/maps/statistics/log_preprocessor/test_data/test_actors, данные - на Sandbox в виде ресурсов.

Конфиги имеют формат JSON и выглядят примерно так:
```
{
    "navigator" : {
        "period": "Day",
        "input": [
            {
                "table": "//home/logfeller/logs/navi-metrika-mobile-log/1d/2020-12-26",
                "file": "navi_input.yson",
                "schema": "navi_input.schema"
            },
            {
                "table": "//home/logfeller/logs/appmetrica-location-log/1d/2020-12-26",
                "file": "navi_location_input.yson",
                "schema": "navi_location_input.schema"
            }
        ],
        "output": [
            {
                "table": "//home/maps/analytics/logs/cooked-metrika-mobile-log/navi/garbage/2020-12-26",
                "file": "garbage.yson"
            },
            {
                "table": "//home/maps/analytics/logs/cooked-metrika-mobile-log/navi/2020-12-26",
                "file": "navi_output.yson"
            }
        ]
    }
    ...
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

При запуске тестов происходит следующее:
1. С Sandbox-а выкачиваются входные и выходные данные
2. Поднимается локальный YT
3. В соответствие с конфигом загружаются исходные таблицы
4. В локальном YT запускается препроцессора
5. Проверяется, совпадают ли выходные таблицы с эталонными выходными таблицами.
  Если обнаружились расхождения - тест фейлится и таблица, получиваяся в результате запуска сбрасывается в папку tests/test-results

### Запуск тестов
Запуск тестов:
```
    ya make -tA --test-stderr
```

При разработке намного удобнее, когда тестовые данные лежат не на Sandbox, а локально. Путь к папке с тестами можно указать в параметре "test_root":
```
    ya make -tA --test-stderr --test-param test_root=path_to_my_test_root
```
В test_root все данные должны лежать в директориии LogPreprocessor, названных так же, как и акторы.
Если в test_root есть данные не для всех акторов, перечисленных в списке акторов (--test-param actors) - запуск завершится ошибко

### Изменение тестов
1. Создать (или скачать с сендбокса текущие) тестовые входные таблицы в формате json и поместить их в директорию test_root/LogPreprocessor
2. Запустить тест
```
    ya make -tA --test-stderr --test-param test_root=path_to_my_test_root
```
4. Тест зафейлится, результат работы актора будет сброшен в tests/test-results
5. Результат из tests/test_actors/test-results перенести в test_root/LogPreprocessor
6. Загрузить test_root/LogPreprocessor на Sandbox. Важно! не забыть указать бесконечный ttl:
```
    ya upload LogPreprocessor --ttl inf
```
7. Добавить ID ресурса в tests/ya.make

## Релиз новой версии
После того, как код закоммичен в Аркадию, релиз делается так:
1. Надо в Sandbox запустить задачу типа
        MAPS_BUILD_STATISTICS_LOG_PREPROCESSOR_V2
После завершения работы все изменения будут подхвачены тестингом
2. Когда решили, что все хорошо работает, жмём кнопку RELEASE у нашей таски MAPS_BUILD_STATISTICS_LOG_PREPROCESSOR_V2

## Откат поломанной версии
Если все же что-то пошло не так, то надо заново запустить MAPS_BUILD_STATISTICS_LOG_PREPROCESSOR_V2, указав ревизию Аркадии, где все ещё было хорошо.
Таска отрабатывет, релизим, и, тем самым, откатываем сломанную версию из стейбла до рабочей
