* `_id`
    * type: str
    * Уникальное имя метрики (`requests_volume`)
* absolute
    * type: str
    * ??? (`requests_volume`)
* agg_func
    * type: str
    * ??? Не используется на беке. 
    Предположительно используется фронтендом только для построения хитмапов (`SUM` или `AVG`) 
* class_any_exists
    * type: bool
    * Флаг проставляется неаддитивным метрикам для которых 
    в базе есть предрасчитанное поле при классе машин``'any'`` 
* color
    * type: str
    * frontend property
    * Свойство задает цвет метрики на графике (`#4651a0`)
* database
    * type: str
    * база данных в ClickHouse, где хранится метрика (`atlas_orders`)
* db
    * type: list[str]
    * LEGACY
    * frontend property
    * пример: `['pixel', 'realtime']`
* default
    * type: bool
    * frontend property
    * ???
* default_leaderboard
    * type: bool
    * frontend property
    * ???
* default_uber
    * type: bool
    * LEGACY
    * frontend property
    * ???
* desc
    * type: str
    * Опциональное поле с описанием метрики
* desc_en
    * type: str
    * Опциональное поле с описанием метрики на английском
* divide_by
    * type: number
    * LEGACY? Выглядит как что-то лишнее, т.к нужную 
    конвертацию можно делать в самом запросе 
    * frontend property
    * Если это свойство есть у метрики, 
    то для отображения на фронте производится деление
    на заданное число. 
        * Пример использования: supply_hours посчитали в секундах, 
        задаем ``divide_by = 3600.0``, получаем часы на фронтенде 
* en
    * type: str
    * frontend property
    * Англоязычный вариант свойства metric
* formula
    * type: str
    * LEGACY
    * Используется только в метрике `supply_hours_efficiency`, 
    причем скорее всего не работает
* ifnull
    * type: number 
    * При получении `null` значения метрики, заменяет его на 
    значение в этом поле (на фронте)
    * ??? В чем смысл
* main_class_if_any
    * type: bool
    * frontend property
    * Если флаг выставлен в `true`, то при выборе `any` в селекторе car_class
    `any` подменяется значением `main_class` для выбранного города
* map
    * type: bool
    * frontend property
    * ???
* metric
    * type: str
    * Название метрики на русском
* metrics
    * type: list[str]
    * ???
* monitoring
    * type: bool
    * ???
* need_final_clause
* optgroup
* optgroup_en
* primary
    * frontend property
* relative
* selection_rules
* selections_0
* selections_1
* selections_2
* selections_3
* server
* server_name
* signal = 'posit
* skip_primary_keys
* table
* target
    * type: number
* var_geohash
* version
    * type: number
    * Версия api, в котором участвует метрика
* sql_query
    * Структурированный способ задать шаблон для Метрик-2.0
* sql_query_raw
    * type: str
    * Строка с шаблоном запроса для Метрик-2.0