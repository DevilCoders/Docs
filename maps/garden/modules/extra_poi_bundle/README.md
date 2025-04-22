# extra_poi_bundle

Регистрирует в Огороде таблицы с организациями, которые хранятся в директории [//home/maps/poi/extra_poi_bundle](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/extra_poi_bundle&)

Датасет состоит их двух таблиц:
* `data` - содержит основные дисплей классы
* `experiments` - содержит альтернативные дисплей классы, необходимые для проведения АБ-экспериментов

Обе таблицы содержат организации как присутствующие, так и отсутствующие в Народной карте.

Модуль готовит таблицы для объединения с ymapsdf:
* таблицы `data` и `experiments` объединяются в одну таблицу `all_data`
* таблица `experiments` копируется без изменений

Результирующие таблицы хранятся в директории [//home/maps/core/garden/prod/extra_poi_bundle](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/extra_poi_bundle&)
