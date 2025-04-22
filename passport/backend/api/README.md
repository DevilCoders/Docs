# Passport API

Основное API Паспорта

## Правила разработки

* Каждый коммит должен быть связан с тикетом в очереди [PASSP](https://st.yandex-team.ru/PASSP). Имена коммитов пишем по-русски и с большой буквы.
* Для нового кода должно быть 100% покрытие тестами.
* Не мокай переводы из Танкера (спросите у коллег если непонятно что это такое).
* При логгировании пользуйся [паспортным style guide по логам](https://wiki.yandex-team.ru/passport/log-style-guide/).
* Разрабатывая новый модуль, позаботься о том, чтобы "тяжелые" операции, например, connect-ы к БД, подгрузка грантов или данных геобазы, были проинициализированы на стадии запуска приложения, а не в момент первого обращения к приложению.
* Оставляй после себя код лучше, чем он был до твоего прихода. Видишь баг - исправь. Можешь стиль улучшить? Сделай это.

## Нагрузочное тестирование

[Sandbox задача](https://sandbox.yandex-team.ru/scheduler/9380/view) запуска стрельбы.
[Панель](https://lunapark.yandex-team.ru/regress/PASSP?service=passport_api_frontend) с результатом стрельбы.

Тестирование автоматически запускается каждую ночь.

## Правила выкладки кода в продакшн

https://wiki.yandex-team.ru/passport/releasesguide


## FAQ
1. Как завести новый SID, для которого при подписке необходимо делать только проверку, есть подписка или нет.
   * Добавить этот сервис в список [настоящих](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/services/services.py?rev=7221952#L95)
или [служебных](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/services/services.py?rev=7221952#L174) сервисов с описанием.
   * Уточнить, есть ли ограничения для данного сида (подписывается через admsubscribe, должен иметь логин и т.д.) и при необходимости добавить в соответствующие [списки](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/services/services.py?rev=7221952#L234)
   * Добавить в [маппинг атрибутов для новой схемы](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/eav_type_mapping/eav_type_mapping.py?rev=7221952#L10). Значение брать из [wiki](http://wiki.yandex-team.ru/passport/dbmoving).
   * Добавить получение значения [поля subscription.suid.SID из ЧЯ](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/api/settings/blackbox_fields.py?rev=7221952).
   * Если подписка запрашивается через аттрибут, то скорее всего вам не нужно запрашивать новые гранты (уточни в [wiki](https://wiki.yandex-team.ru/passport/dbmoving)).
   * Если все же нужны гранты, то следует запросить их в ЧЯ (во всех окружениях, в том числе и в yateam) на `subscription.suid.SID`,
создав тикет в [st/PASSPORTGRANTS](https://st.yandex-team.ru/createTicket?queue=PASSPORTGRANTS).
   * Если сид блокирующий, то после влития пулла пересобрать и перевыкатить [dbscripts](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/dbscripts). Также желательно обновить список блокирующих сидов в коде админки.
2. Как добавить новый хост:
   * Добавить новый хост в [список HOSTS](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/api/settings/hosts.py?rev=7221952#L10), не забыв указать id и датацентр
   * Добавить хост в [конфигурацию локальных редисов _REDIS_CONFIG](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/api/settings/redis.py?rev=7221952#L25) в соответствующее окружение
   * В случае добавления нового ДЦ нужно добавить хост с редис-счетчиком: добавить соответствие <дц>:<хост-ид> в [маппинг _COUNTERS_REDIS_MANAGERS](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/api/settings/counters/__init__.py?rev=7284536#L100) в соответствующее окружение
3. Как добавить новый атрибут.
   * Добавить имя атрибута в нужный [список BLACKBOX_*_ATTRIBUTES](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/api/settings/blackbox_fields.py?rev=7221952).
   * Добавить атрибут и его номер в [ATTRIBUTE_NAME_TO_TYPE](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/eav_type_mapping/eav_type_mapping.py?rev=7221952#L10).
   * Если нужно автоматическое приведение значения к int, то добавить имя атрибута в [_BLACKBOX_ATTRIBUTES_INTEGER_FIELDNAMES](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/builders/blackbox/parsers.py?rev=7221952#L88).
   * Обновить парсер нужной модели (https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/models).
   * Добавить атрибут в EAV_FIELDS_MAPPER у подходящего сериализатора (https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/serializers/eav)
   * Настроить сериализацию в [historydb](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/serializers/logs/historydb/serializers.py) и (опционально) [statbox](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core/serializers/logs/statbox/serializers.py)
   * Если атрибут требует грантов, то указать это на [вики](https://wiki.yandex-team.ru/passport/dbmoving), а также [запросить гранты](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/api/settings/blackbox_fields.py?rev=7221952#L213)
