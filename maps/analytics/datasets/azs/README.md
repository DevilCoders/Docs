# Датасет АЗС

Содержит информацию о всех АЗС

| Сервис | Ссылки |
|:------------- |:-------------:|
| Таблицы на YT | [//home/maps/analytics/datasets/azs](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/azs)

[comment]: <> (| Отчеты в Статистике | [Мобильные карт]&#40;https://stat.yandex-team.ru/-/CCUYZHD8TC&#41;)

[comment]: <> (| Фичи и метрики | [arcadia/maps/analytics/metrics/routes]&#40;https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/metrics/routes&#41;)

[comment]: <> (| Датасет в Datalens | TBD)

## Примеры расчетов по датасету

[comment]: <> (* [Посчитать]&#40;https://yql.yandex-team.ru/Operations/YILmOwPTTiVjLezNK3KwYCSN2QVkTGfKYYe_scQ3Uvs=&#41; базовую воронку по каждому типу маршрута)

[comment]: <> (* [Достать]&#40;https://yql.yandex-team.ru/Operations/YILnIr94hv4LoJEHD5li1OeVWtWcUisPFen7SEgORmA=&#41; координаты точки А)

## Описание полей

| Поле | Физический смысл |
|:-------------| -------------|
| `permalink` | Пермалинк из справочника|
| `chain_id` | Id сети из справочника|
| `chain_name` | Название сети из справочника|
| `geo_id` | Id Наименьшего региона из геобазы |
| `head_permalink` | head_permalink из справочника|
| `lat` |  Широта из справочника |
| `lon` | Долгота из справочника |
| `name` | Название АЗС из справочника|
| `main_rubric_id` | Id рубрики из справочника |
| `publishing_status` | Опубликована в алтае |
| `normal_name` | Нормализованное поле name |
| `station_id` | Id АЗС из базы ЯЗ |
| `bonus_card_name` | Название программы лояльности |
| `сolumns_number` | Количество колонок на АЗС |
| `сompany_id_corporation` | Id компании для корпоративных клиентов |
| `сompany_name_corporation` | Название компании для корпоративных клиентов |
| `company_id_individual` | Id компании для физических лиц |
| `company_name_individual` | Название компании для физических лиц |
| `fuels` | структура с типом топлива по колонкам |
| `station_name` | Название АЗС из базы Заправок |
| `name_map` | Название, которое отображается на карте |
| `network_id` | Id сети из базы Заправок|
| `polygon` | Структура, содержащая полигон |
| `post_pay` | Тип оплаты на АЗС (постоплата или предоплата) |
| `yandex_station_device` | Id Яндекс.Станции на АЗС |
| `soft` | ПО, по которому подключена АЗС к Яндекс Заправкам |
| `network_name` | Название сети АЗС из базы Заправок |
| `integration` | Тип подключения АЗС к Яндекс Заправкам (планшет, интеграция) |
| `station_stable` | Доступна ли АЗС пользователям в Навигаторе как АЗС, где можно оплатить топливо |
| `normal_name_map` | Нормализованное название АЗС |
| `date_create` | Дата подключения к ЯЗ |


## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или lincnitnastya@

