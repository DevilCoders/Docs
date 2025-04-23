# Что где лежит

## Бизнес-сущности

Сущность | БД | Таблица/путь | Комментарий
:--- | :--- | :--- | :---
Маппинг|PG|`mdm.mappings_cache`| [Привязки](../newbie/second_steps.md#mappings) SSKU к MSKU и категориям
Серебро SSKU|Yt|`//home/market/production/mdm/storage/ssku_silver`| [Исходные данные](../newbie/second_steps.md#silver) по SSKU
Старое серебро SSKU|PG|`mdm.from_iris_item`| Исходные данные по SSKU от складов, устарели
Электрум SSKU|PG|`mdm.master_data`| Серебро и золото SSKU в одном флаконе для большинства мастер-данных кроме ВГХ
Золото SSKU #1|PG|`mdm.reference_item`| [Золото](../newbie/second_steps.md#gold) SSKU по ВГХ
Золото SSKU #2|PG|`mdm.golden_ssku_entity`| Промежуточное золото в [Entity-формате](yt_storage.md#entity), посредник между уровнями MSKU и SSKU
MSKU|Yt|`//home/market/production/mdm/storage/msku_gold`| Одновременно серебро и золото для [MSKU](../newbie/second_steps.md#msku)
Партнёрские вердикты|Yt|`//home/market/production/mdm/storage/silver_ssku_resolution`| Ошибки валидации серебра SSKU
Золотые вердикты|Yt|`//home/market/production/mdm/storage/golden_ssku_resolution`| Ошибки валидации золота SSKU
Склады|Yt|`//home/market/production/mdm/storage/warehouse`| Номера складов и их приоритеты
Копия складов|PG|`mdm.mdm_warehouse_projection`| Копия складов и приоритетов в БД старого МДМ
Дропшипы|PG|`mdm.warehouse`| Детальная информация по складам и их типам
Дерево ТН ВЭД|PG|`mdm.customs_comm_code`| Дерево префиксов ТН ВЭД и разметка оных Честным ЗНАКом
Карготипы|PG|`mdm.cargo_type`| Реестр существующих в Маркете карготипов
Категорийные настройки|PG|`mdm.category_param_value`| Данные уровня [категорий](../newbie/second_steps.md#category)
Категорийные ОСГ|PG|`mdm.category_rsl`| Разметка остаточных сроков годности по категориям. Используется редко.
MSKU ОСГ|PG|`mdm.msku_rsl`| Разметка остаточных сроков годности по MSKU. Используется редко.
SSKU ОСГ|PG|`mdm.ssku_rsl`| Разметка остаточных сроков годности по SSKU. Используется редко.
Партнёрские ОСГ|PG|`mdm.supplier_rsl`| Разметка остаточных сроков годности по поставщикам. Основная разметка ОСГ.
Товарные группы|PG|`mdm.good_group`| Товарные группы категорий, связанных обязательностью маркировки Честным ЗНАКом. Используются грубым классификатором вне МДМ.
Меркурианские хэши|PG|`mdm.mercury_hash`| Хэши отправляемых в Axapta данных, защищающие от дублирующихся отправок
Правила бизнес-мержа|PG|`mdm.merge_settings`| Правила мержа сервисных офферов в [бизнес-оффер](../../contour/business_domain/business_offer.md)
Старые скрытия SSKU|PG|`mdm.offer_cutoff`| Легаси-скрытия офферов по невалидным данным. Почти заменены вердиктами.
Цены|PG|`mdm.price_info`| Цены без учёта НДС для генерации карготипа "Ценное"
Документы|PG|`mdm.quality_document`| Сертификаты, регистрационные документы и отказные письма
Привязки документов|PG|`mdm.offer_document`| Связи между SSKU и документами
Существование сервисов SSKU|PG|`mdm.ssku_existence`| Маркеры существования модели размещения сервисных офферов внутри бизнес-оффера.
Поставщики|PG|`mdm.supplier`| Список партнёров Маркета
Очередь удаления офферов |PG|`mdm.ssku_to_delete`|Отметка о том, что оффер подлежит [удалению](../algorithm/remove_algo.md) в скором будущем.

## Инфраструктурное

Все инфраструктурные таблицы хранятся в PostgreSQL.

Сущность | Таблица/путь | Комментарий
:--- | :--- | :---
История авторазметки|`mdm.auto_markup_history`| История запусков [авторазметки](https://mdm-testing.market.yandex-team.ru/mdm/automarkup)|
Запросы авторазметки|`mdm.auto_markup_yql_query`| Настройки запросов авторазметки|
История liquibase|`mdm.databasechangelog`|Лог выполнения миграций liquibase|
Лок liquibase|`mdm.databasechangeloglock`|Флажок блокировки БД для накатки liquibase-миграций|
Хронология размеров таблиц|`mdm.disk_space_history`|Исторические слепки величины таблиц для построения графиков и удовлетворения любопытства|
История загрузок файлов|`mdm.file_history`|История загрузок MSKU, SSKU и категорийных Excel файлов в МДМ|
Пользователи MBO|`mdm.mbo_user`|Список зарегистрированных в МВО пользователей, используется для авторизации при работе с MSKU|
Пользователи MDM|`metadata.mdm_user`|Список зарегистрированных в MDM пользователей, используется для авторизации в МДМ|
SKV / рубильники |`mdm.storage_key_value`|Пары "Ключ + значение" и [рубильники](../practices/skv.md)|
История крон-джоб |`mdm_tms.qrtz_log`|Логи запусков TMS-джоб МДМ|

## Метаданные из mdm-metadata

Все метаданные хранятся в PostgreSQL.

Сущность | Таблица/путь | Комментарий
:--- | :--- | :---
Настройки отображения|`metadata.common_param_view_setting`|Задают, как рисовать поля ввода в UI для каждого атрибута в МДМ, например, "Строковое read-only поле, пятое по порядку"|
Тип отображения|`metadata.common_view_type`|Список вариантов отображения различных типов сущностей в МДМ|
Атрибуты|`metadata.mdm_attribute`|Список всех атрибутов (полей), которыми обладают объекты в МДМ, например, "Срок годности", "Вес нетто" и др.|
Типы сущностей|`metadata.mdm_entity_type`|Список разновидностей сущностей МДМ, например, "Золотая SSKU", "MSKU" и др.|
Опции enum-ов|`metadata.mdm_enum_option`|Список опций для каждого enum-атрибута в МДМ, например, для атрибута "Цвет" это будут "красный", "синий" и "зелёный"|
Внешние связи|`metadata.mdm_external_reference`|Связи для атрибутов, типов сущностей и опций БМДМа с их аналогами в других подсистемах Маркета|
Мета-деревья|`metadata.mdm_tree_edge`|Конфигуратор деревьев, позволяет строить дерево из чего угодно и отображать в UI|
Копия настроек отображения|`mdm.mdm_common_param_view_setting_projection`|Копия соответствующей таблицы в старом МДМ для быстрого доступа|
Копия типов сущностей|`mdm.mdm_entity_type_projection`|Копия соответствующей таблицы в старом МДМ для быстрого доступа|
Копия внешних связей|`mdm.mdm_external_reference_projection`|Копия соответствующей таблицы в старом МДМ для быстрого доступа|
Старые атрибуты|`mdm.mdm_param`|Устаревшая таблица атрибутов|
Старые настройки отображения|`mdm.mdm_param_io_settings`|Устаревшая таблица настроек отображения|

## Аудит

Аудит содержит историю изменений объектов. Глобально у нас существует аж три различных аудита.

1. Аудит MBO. Строго говоря, это не наш аудит, а МВОшный. Предназначен для хранения истории изменений MSKU и SSKU. Живёт [здесь](https://mbo.market.yandex-team.ru/ui/audit).
2. Старый аудит. Представляет собой омегажирную партицированную таблицу `mdm_audit.audit`, которая регулярными процессами копируется в Yt по пути [//home/market/production/mbo/mdm/audit/mdm_audit_archive](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/mdm/audit/mdm_audit_archive).
3. Новый аудит. Это интегрированные в Yt-хранилища таблички, автоматически заполняемые при любых существенных апдейтах. Всегда лежат рядом с обычными таблицами, но имеют суффикс `snapshot`. Например, для таблицы [MSKU](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/mdm/storage/msku_gold) имеется соответствующая [snapshot-табличка](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/mdm/storage/msku_gold_snapshot).

Более подробно про все виды аудита можно прочитать [здесь](audit.md).
