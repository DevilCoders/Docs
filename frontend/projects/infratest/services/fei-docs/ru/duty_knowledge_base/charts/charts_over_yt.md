# Charts Over YT

## Почему тикеты на графике и в фильтре могут отличаться?

Ключевые слова:

* Очередь не возвращается в фильтре в кликхаусе
* На графике не хватает тикетов из фильтра
* На графике отображаются не все тикеты

Проблемы приводящие к такому поведению:

1. В базе данных нет данных для очереди, на которую ссылается фильтр. Для проверки можно использовать эту [инструкцию](https://wiki.yandex-team.ru/search-interfaces/infra/assessors/chart-docs/#kakproveritnalichiemoixocheredejjuvasvsisteme). Если данных нет, то пользователю требуется пройтись по [инструкции](https://wiki.yandex-team.ru/search-interfaces/infra/assessors/chart-docs/#kakzaprositvygruzkunovojjocheredi).
2. Фильтр добавлен в [словарь](https://stat.yandex-team.ru/DictionaryEditor/fei_cycle_time_filters), но нет доступов к очереди, на которую ссылается фильтр. Пользователю требуется пройтись по [инструкции](https://wiki.yandex-team.ru/search-interfaces/infra/assessors/chart-docs/#kaknachatpolzovatsja).

## Я не нашел ответ на свой вопрос

Попробуйте найти решение на одной из wiki страниц:

* [Решение типовых проблем, связанных с графиками](https://wiki.yandex-team.ru/search-interfaces/infra/assessors/charts)
* [Инструкция по использованию графиков](https://wiki.yandex-team.ru/search-interfaces/infra/assessors/chart-docs)
* [Синхронизация фильтров трекера в CH](https://wiki.yandex-team.ru/search-interfaces/infra/charts/cycletime/filters_sync)

Если не нашли, то обратитесь к эксперту.
