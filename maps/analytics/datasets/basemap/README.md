# Датасет с событиями поев на карте
- [Таблицы на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/datasets/basemap)
- [Датасет в Datalens](https://datalens.yandex-team.ru/datasets/gbb5tdzdmn3gc-basemap)

## Примеры расчетов по датасету

* [Посчитать](https://yql.yandex-team.ru/Operations/YDC49NK3DP9VRHF_hHmqswrJvizWgL1COBXnYPw2E6k=) общее кол-во открытий, открытия с deep use, открытия геопродукта;
* [Посчитать](https://yql.yandex-team.ru/Operations/XwxQcJ3udkiRg5LGzENueRmFhNsTZDImMBrX8T2-MNQ=) открытия по зумам;
* [Посчитать](https://yql.yandex-team.ru/Operations/XwxQeBpqv-RDuss6eiYfPKuJk5iP2UorejVKF8aoAgQ=) открытия по классу рубрик;

## Отчеты и дашборды по датасету

* [Отчет](https://stat-beta.yandex-team.ru/Multiproject/datasets/basemap) c метриками подложки;


## Назначение
* Хранит в себе события открытия карточек организации при клике по пои и список совершенных действий пользователем на этой карточке
* Одна строка - факт открытия карточки при клике по пои для определенного набора `(uri, reqid, user_id)`

## Для каких сервисов считается

* [Веб-карты](web-maps/query.sql)
* [Мобильные карты](mobile-maps/query.sql)

## Источники

| Сервис | Источник | Что забираем |
|:------------- |:-------------:| -------------:|
| Веб-карты | Логи веб карт, очищенные внутренним антифродом [cooked-bebr-log](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/logs/cooked-bebr-log/desktop-maps/clean&)  | Отбираем события открытия карточки пои ( `'%poi%.preview_card', '%poi%.collapsed_card'`  с типом события `show`) и клика по пои (`'maps_www.map.poi_layer'` и `'maps_www.map.indoor_layer'` с типом события `click`). Отдельно берем события кликов внутри открытой карточки.
| Мобильные карты | Логи мобильных карт [cooked-app-metrics-log](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/logs/cooked-appmetrica-log/mobile-maps&) | Отбираем события открытия карточки пои (`'search.show-place-card', 'search.open-place-view'`) и клика по пои (`'map.select-poi'`). Отдельно берем события кликов внутри открытой карточки.
| Общее | Картографические объекты [ft](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/ft&) | По полю `icon_class` отбираем признак `super_poi`
| Общее | Источники картографических объектов [ft_source](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/ft_source&) | По полю `source_type_id` фильтруем только объекты, источником которых является организации из sprav.yandex.ru
| Общее | Классификации рубрик [rubrics](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/analytics/data/rubrics-classification&) | Используем, чтобы определить класс главной рубрики и ее название
| Общее | Информация по организациям [company_pretty_format](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/assay/common/company_pretty_format&) | Берем оттуда основную информацию по организациям (география, название, id главной рубрики)

## Схема расчета

1. Выгружаем логи с нужными событиями из источников (файл lib/yql_library.sql)
2. Оставляем только те открытия, которые последовали после клика по пои. Для этого смотрим на временнУю задержку между кликом и открытием карточки, она не должна быть больше определенного временного промежутка. Для каждого сервиса эмпирическим путем был подобран свой подходящий временной промежуток. (файл query.sql)
3. Выгружаем отдельно все события из логов, которые не являлись открытием карточки или кликом по пои.(файл query.sql)
4. Джоиним клики внутри карточки из п.3 на факты открытия карточек из п.2 по `(user_id, oid, reqid)`.(файл query.sql)
5. Производим классификацию событий кликов внутри карточки, считаем количество каждых событий, определяем DU, GDU и другое.(файл common.sql)

## Модель данных и описание полей

**Описание полей**

|  | Поле              | Физический смысл                                                                                                                                                                                                                                           | Источник |
|:------------- |:------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| 1| user_id           | Идентификатор пользователя yandexuid для веб-карт, uuid для приложений                                                                                                                                                                                     | cooked-bebr-log cooked-metrika-mobile-log |
| 2| lat               | координаты объекта,широта                                                                                                                                                                                                                                  | company_pretty_format |
| 3| lon               | координаты объекта,долгота                                                                                                                                                                                                                                 | company_pretty_format |
| 4| os                | ОС устройства                                                                                                                                                                                                                                              | cooked-bebr-log cooked-metrika-mobile-log |
| 5| has_deep_use      | Был ли [deep use](https://wiki.yandex-team.ru/geo/dashboard/glossary/#deepuse) у карточки. Определяется [списком](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/geo/maps/common/clicks_extractor.py?rev=7073404#L101) префиксов для каждого сервиса | вычислимое|
| 6| events            | список событий по ключу (reqid, uri) отсортированных по timestamp                                                                                                                                                                                          | вычислимое |
| 7| permalink         | ID, пермалинк организации                                                                                                                                                                                                                                  | cooked-bebr-logcooked-metrika-mobile-log
| 8| zoom              | зум, на котором произошел клик по карточке                                                                                                                                                                                                                 | cooked-bebr-logcooked-metrika-mobile-log |
| 9| event_geoid       | geoid пользователя в момент совершения события                                                                                                                                                                                                             | cooked-bebr-logcooked-metrika-mobile-log |
| 10| main_rubric_class | главный класс рубрики                                                                                                                                                                                                                                      | //home/maps/analytics/data/rubrics-classification |
| 11| main_rubric_id    | id главной рубрики                                                                                                                                                                                                                                         | company_pretty_format |
| 12| test_buckets      | https://wiki.yandex-team.ru/JandeksPoisk/TematicheskiePoiski/GeoPoisk/metrics/mapreqanslog/#test_buckets                                                                                                                                                   | cooked-bebr-logcooked-metrika-mobile-log |
| 14| chain_name        | название сети                                                                                                                                                                                                                                              | company_pretty_format |
| 15| puid              | уникальный идентификатор пользователя в Яндекс.Паспорте, выдаваемый всем при регистрации аккаунта в яндексе                                                                                                                                                | cooked-bebr-logcooked-metrika-mobile-log|
| 16| uri               | идентификатор геообъекта                                                                                                                                                                                                                                   | cooked-bebr-logcooked-metrika-mobile-log |
| 18| is_super_poi      | является ли иконка объекта на карте Super poi                                                                                                                                                                                                              | //home/maps/core/garden/stable/ymapsdf/latest/cis1/ft |
| 18| is_personal       | является ли POI персональным (логируем информацию в клике)                                                                                                                                                                                                 |
| 19| reqid             | https://wiki.yandex-team.ru/JandeksPoisk/TematicheskiePoiski/GeoPoisk/metrics/mapreqanslog/#reqid                                                                                                                                                          |
| 20| log_date          | дата расчета                                                                                                                                                                                                                                               | |
| 21| main_rubric_name  | название главной рубрики                                                                                                                                                                                                                                   | //home/maps/analytics/data/rubrics-classification |
| 22| name              | название объекта, по которому произошел клик                                                                                                                                                                                                               | company_pretty_format |
| 24| chain_id          | id сети                                                                                                                                                                                                                                                    | company_pretty_format |
| 25| geoid             | самый детальный geoid объекта                                                                                                                                                                                                                              | company_pretty_format |
| 26| session_id        | 	Идентификатор сессии пользователя в сервисе (неуникальный)                                                                                                                                                                                                | cooked-bebr-logcooked-metrika-mobile-log |
| 27| is_geoproduct     | является ли геопродуктом                                                                                                                                                                                                                                   | |
| 28| timestamp         | время события (в секундах)                                                                                                                                                                                                                                 | cooked-bebr-logcooked-metrika-mobile-log |

## К кому можно обращаться с вопросами

Вопросы задавать можно в чат поддержки аналитики в [Slack](https://join.slack.com/share/zt-jfgq9obr-8WV8gxokWri3A1wa9TrBjg?cdn_fallback=1) или ikolodin@

