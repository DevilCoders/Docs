# Непрерывный профайлер

_Непрерывный профайлер_ позволяет держать профайлер постоянно включенным с минимальным оверхедом.

Он доступен по умолчанию всем приложениям из verticals-backend, которые наследуются от BaseApp.

Если используется свой базовый класс для инициализации приложения, то включить профайлер можно с помощью класса [`common.zio.app.profiler.ProfilerInit`](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/common/zio/app/profiler/ProfilerInit.scala).

Для включения профайлера необходимо объявить переменную окружения `PROFILER_MODE` с необходимым режимом работы.

Пример: [https://a.yandex-team.ru/arcadia/classifieds/services/deploy/profiler-collector.yml?rev=r9749509#L36](https://a.yandex-team.ru/arcadia/classifieds/services/deploy/profiler-collector.yml?rev=r9749509#L36)

## Режимы работы

Можно включить сразу несколько режимов профайлера, для этого надо указать эти режимы через запятую.

При этом разные режимы профилирования cpu и perf-событий не могут работать одновременно.

Рекомендуемый режим работы — `cpu,alloc`

Доступные режимы работы:

-   **cpu** — профилирование cpu используя perf events
-   **itimer** — профилирование cpu используя системный таймер
-   **wall** — профилирование cpu используя отдельный спящий поток
-   **\<name\>** — профилирование произвольного perf event
-   **alloc** — профилирование аллокаций памяти
-   **locks** — профилирование синхронизаций и блокировок

## Просмотр результатов

Смотреть результаты профилирования можно по адресам:
Прод: [https://profiler.vertis.yandex-team.ru/flame-graph](https://profiler.vertis.yandex-team.ru/flame-graph) \
Тестинг и дев: [https://profiler.test.vertis.yandex-team.ru/flame-graph](https://profiler.test.vertis.yandex-team.ru/flame-graph)

Параметры:

-   **service** — имя сервиса (_обязательный параметр_)
-   **from**=_-10m_, **to**=_now_ — начало и конец интервала. можно указать абсолютное время (Пример: `2022-07-27T10:00:00Z`) и интервал относительно текущего момента (Примеры: `-1h`, `-15m`, `-30s`, `now`).\
    По умолчанию `-10m` и `now` соответственно.
-   **mode**=_cpu_ — режим работы профайлера который надо показать. По умолчанию `cpu`
-   **reverse**=_(true|false)_ — инвертировать флеймграф
-   **lines**=_(true|false)_ — показывать имена строк рядом с именем функции
-   **minwidth**= — минимальная ширина столба во флеймграфе в процентах от общей ширины; стектрейсы меньше этой ширины не будут показываться. Позволяет упростить флеймграф.
-   **\<label\>** — остальные параметры парсятся как фильтры по метаданным, которые присылает профайлер на сервис.

Метаданные посылаемые профайлером по умолчанию:

-   **dc** — датацентр
-   **allocation_id** — id инстанса приложения
-   **version** — версия приложения
-   **branch** — имя ветки (или пустая строка)
-   **hostname** — имя хоста, где выполняется программа
-   **layer** — окружение (prod, test, dev)

Примеры:

-   cpu в сервисе `broker-pipeline-lb-yt` за последний час, со столбиками больше 1 процента [(ссылка)](https://profiler.vertis.yandex-team.ru/flame-graph?service=broker-pipeline-lb-yt&mode=cpu&minwidth=1&from=-1h)
-   аллокации в сервисе `profiler-collector` в сасово [(ссылка)](https://profiler.vertis.yandex-team.ru/flame-graph?service=profiler-collector&mode=alloc&dc=sas)
