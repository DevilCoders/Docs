# Порядок и сроки удаления данных пользователей


## Удаление ресурса при получении запроса через API сервиса {#api}

Если сервис получает запрос на удаление ресурса через API, ресурс немедленно помечается как удаляемый и не может быть восстановлен. Фактически удаление производится в течение 72 часов.


## Автоматическая блокировка облака {#block}

{% if product == "yandex-cloud" %}

Ваше облако может быть заблокировано при наличии задолженности, при завершении пробного периода или при нарушении [условий использования {{ yandex-cloud }}]{% if lang == "ru" %}(https://yandex.ru/legal/cloud_termsofuse/?lang=ru){% endif %}{% if lang == "en" %}(https://yandex.ru/legal/cloud_termsofuse/?lang=en){% endif %}. Подробнее о процессе оплаты и возможной блокировке читайте в документации Биллинга, в разделе **Цикл оплаты**:
* [Физическим лицам](../../billing/payment/billing-cycle-individual.md)
* [Организациям и ИП](../../billing/payment/billing-cycle-business.md)

{% endif %}

{% if product == "cloud-il" %}

Ваше облако может быть заблокировано при нарушении [условий использования {{ yandex-cloud }}](../../legal/terms).

{% endif %}

В заблокированном облаке:

1. Останавливаются виртуальные машины и другие ресурсы, но данные не удаляются. В течение {% if product == "yandex-cloud" %}60 дней (при нарушении условий использования — 7 дней){% endif %}{% if product == "cloud-il" %}7 дней{% endif %} облако можно разблокировать, а остановленные ресурсы — запустить.
2. По истечении этого срока {{ yandex-cloud }} может пометить ресурсы как удаляемые и безвозвратно удалить их вместе с данными в течение 72 часов.


## Удаление логов запросов к ресурсам {#logs}

Записи о запросах к ресурсам пользователя через API хранятся в течение года для анализа инцидентов информационной безопасности и противодействия мошенничеству.

По истечении года записи безвозвратно удаляются.


## Удаление облака пользователя {#cloud}

При удалении облака:

1. Останавливаются запущенные в облаке виртуальные машины и другие ресурсы, но данные не удаляются. В течение 30 дней облако можно восстановить вместе с ресурсами.
2. Если облако не было восстановлено в течение 30 дней, ресурсы во всех сервисах помечаются как удаляемые и удаляются в течение 72 часов.

При разрыве контракта все облака пользователя и ресурсы в них немедленно помечаются как удаляемые и удаляются в течение 72 часов.


{% if product == "yandex-cloud" %}

## Удаление платежного аккаунта {#billing-account}

Удалить [платежный аккаунт](../../billing/concepts/billing-account.md) можно только если к нему не привязаны облака, и только при обращении в техническую поддержку.

1. После запроса пользователя платежный аккаунт помечается как удаляемый и в течение 72 часов перестает быть доступен пользователю.
2. Информация о платежном аккаунте может использоваться для формирования финансовой отчетности. Поэтому эта информация хранится до истечения срока исковой давности и срока, установленного применимым финансовым законодательством.
3. По истечении указанных сроков платежный аккаунт удаляется без возможности восстановления.

{% endif %}
