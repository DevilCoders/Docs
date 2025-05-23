# Statist

## Назначение
Сервис представляет из себя API над кликхаусом для подсчета самых простых агрегатов – различного рода счетчиков. То есть вместо того, чтобы инкрементить счетчики, статист получает их значения непосредственно из агрегатов над сырыми данными в кликхаусе. Таким образом, если требуется добавить еще один разрез/счетчик над теми же данными, то не требуется накликивать новые счетчики. Достаточно просто построить нужный агрегат в clickhouse.

## Реализация
Высокоуровнево это выглядит так:

- сырые события поставляются в clickhouse через брокер (еще есть старые поставки через db-transmitter-streamer). Пишется каждое событие, но не все поля, потому что место в ch дорого.
- с помощью materialized view кликхауса данные автоматически раскладываются в таблички-агрегаторы с движком из семейства [*MergeTree](https://clickhouse.tech/docs/ru/engines/table-engines/#mergetree)
- статист предоставляет апи для получение данных из таблиц-агрегаторов.

Фактически, статист не знает ничего о том, как формируются таблицы-агрегаторы. Так что первые два пункта – это просто то, как это сделано сейчас. При желании можно сделать другой пайплайн доставки данных. Плюс статист может сам вычислять суммы напрямую из сырых данных, но это не очень эффективно.

#### Кэширование
Точечные значения счетчиков кэшируются. Кэш используется не только по прямому назначению (для ускорения доступа), но так же для фоллбэка в случае, если clickhouse отвечает медленно или недоступен.  
В качестве кэша используется Redis в MDB (изначально был couchbase, о съезде [тут](https://st.yandex-team.ru/VSDATA-1433))

## У нас есть чатик

https://t.me/joinchat/VD2z3bkPo3WNDNen

## И очередь

https://st.yandex-team.ru/VSDATA

Чтобы создать тикет на заведение нового счётчика, заполните [форму](https://forms.yandex-team.ru/surveys/73406/).
Туда можно подробно описать какой счётчик вам нужен, и мы его (когда-нибудь) сделаем.

## Поддержка
[Как создать счетчик](./docs/counters.md)

[Как перелить историю](./docs/history.md)
## Ссылочки

* [Не очень полезная дока по кликхаусу](https://clickhouse.tech/docs/ru)
* [Полезная инфа чтобы понять мат вью](https://den-crane.github.io/Everything_you_should_know_about_materialized_views_commented.pdf)
* [Внешний (!) чат, в котором могут помочь](https://t.me/clickhouse_ru)
* [Внешний (!) чат, в котором могут помочь на английском](https://t.me/clickhouse_en)
