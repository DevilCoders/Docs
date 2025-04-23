# Датасет заказов показов POI
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/datasets/poi-shows)



## Назначение

Хранит данные о показах POI и длительности показов в сервисах МЯК, нави, веб-карты, мобильные веб-карты


## Источники

- Cooked логи соответствующих сервисов из папки [maps/analytics/logs](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/logs)
- таблица доходов геопродукта: [money/revenue](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/geoadv/geoproduct/money/revenue)
## Схема расчета

Для нави и МЯК используется [событие](https://st.yandex-team.ru/MAPSMOBCORE-12164) длительности показа POI из mapkit

Для веб сервисов использутся как события показа POI (не содержащие временм показа) так и события скрытия (содеражащие вермя показа), в случае если залогирован показ, но не залогировано скрытие время показа записыватся как минимально гарантированное 0 милисекунд

## Модель данных и описание полей
Таблицы считаются ежедневно

Таблицы уникальны по столбцам device_id, session_id, permalink. Т.е. одна строчка это все показы одного пермалинка в одной сессии одного пользователя

### Для мобильных приложений
|     | Поле                   | Значение                                                                 | Источник                                                             |
|:----|:-----------------------|:-------------------------------------------------------------------------|----------------------------------------------------------------------|
| 1   | device_id              | DeviceID пользователя                                                    | Поле DeviceID из cooked logs                                         |
| 2   | session_id             | SessionID пользователя                                                   | Поле SessionID из cooked logs                                        |
| 3   | permalink              | Пермалинк организации показонного POI                                    | Значение из map.poi_display_duration_base64                          |
| 4   | layer_id               | Был ли показанный POI персонализированным                                | Значение из map.poi_display_duration_base64                          |
| 5   | is_personal        | Был ли показанный POI персонализированным                                | Значение из map.poi_display_duration_base64                          |
| 6   | display_duration_in_ms | Длительность показа POI в милисекундах                                   | map.poi_display_duration_base64                                      |
| 7   | shows_in_session       | Количество показов POI в сессии                                          | Количество появлений в map.poi_display_duration_base64               |
| 8   | service                | Сервис нави или мяк                                                      | Берется из аргументов расчета                                        |
| 9   | log_date               | Дата прихода лога (в строке)                                             | Берется из аргументов расчета, совпадает с именем исходной таблицы   |
| 10  | user_id                | Дублирует колонку device_id для консистентности расчетов разных сервисов | Дублирует колонку device_id                                          |
| 11  | session_date           | Дата прихода лога (в строке)                                             | Приведенное поле StartTimestamp из cooked logs                       |
| 12  | test_buckets           | Тест бакеты пользователя                                                 | Поле TestBuckets из cooked logs                                      |
| 13  | geoid            | География пользователя                                                   | Поле RegionID из cooked logs                                         |
| 14  | os                     | ОС устройства                                                            | Поле AppPlatform из cooked logs                                      |
| 15  | uuid                   | UUID пользователя                                                        | Поле UUID из cooked logs                                             |
| 16  | puid                   | PUID пользователя                                                        | Поле AccountID из cooked logs                                        |
| 17  | app_version_name       | AppVersionName пользователя                                              | Поле AppVersionName из cooked logs                                   |
| 18  | is_branded             | брендированный ли POI                                                    | 1, если campaign_package_type='Супербрендирование' в таблице доходов |
| 19  | geo_campaign_id        | идентификатор рекламной кампании                                         | Поле geo_campaign_id из таблицы доходов                              |

### Для веб сервисов

|     | Поле                   | Значение                                                                 | Источник                                                                            |
|:----| :--------------------- | :----------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| 1   | yandexuid              | yandexuid пользователя                                                   | Поле yandexuid из cooked logs                                                       |
| 2   | session_id             | sesion_id пользователя                                                   | Поле sesion_id из cooked logs                                                       |
| 3   | permalink              | Пермалинк организации показонного POI                                    | Значение из maps_www.map.poi_layer (pois,uri)                                       |
| 4   | is_personal        | Был ли показанный POI персонализированным                                | Значение из maps_www.map.poi_layer (pois,personal)                                  |
| 5   | display_duration_in_ms | Длительность показа POI в милисекундах                                   | Если есть 'poi_hide' Значение из maps_www.map.poi_layer (pois,viewingTime), иначе 0 |
| 6   | shows_in_session       | Количество показов POI в сессии                                          | Количество появлений в maps_www.map.poi_layer 'poi_show'                            |
| 7   | service                | Сервис десктоп или тач                                                   | Берется из аргументов расчета                                                       |
| 8   | log_date               | Дата прихода лога (в строке)                                             | Берется из аргументов расчета, совпадает с именем исходной таблицы                  |
| 9   | user_id                | Дублирует колонку yandexuid для консистентности расчетов разных сервисов | Дублирует колонку yandexuid                                                         |
| 10  | session_date           | Дата прихода лога (в строке)                                             | Поле session_date из cooked logs                                                    |
| 11  | test_buckets           | Тест бакеты пользователя                                                 | Поле test_buckets из cooked logs                                                    |
| 12  | geoid            | География пользователя                                                   | Поле geo_id из cooked logs                                                          |
| 13  | os                     | ОС устройства                                                            | Поле parsed_os из cooked logs                                                       |
| 14  | puid                   | PUID пользователя                                                        | Поле puid из cooked logs                                                            |
| 15  | is_branded             | брендированный ли POI                                                    | 1, если campaign_package_type='Супербрендирование' в таблице доходов |
| 16  | geo_campaign_id        | идентификатор рекламной кампании                                         | Поле geo_campaign_id из таблицы доходов                              |
|  17   | min_zoom                 | миниальный зум poi за сессию  |  zoom из maps_www.map.poi_layer     |
|  18   | max_zoom               |  максимальный зум poi за сессию|   zoom из maps_www.map.poi_layer      |
|  19   | first_zoom               | первый зум poi за сессию |    zoom из maps_www.map.poi_layer     |

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или andrey-shan@, itangaev@.
