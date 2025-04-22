{% cut "X-Ya-Service-Ticket" %}

[Service-тикет TVM](https://wiki.yandex-team.ru/passport/tvm2/stbrief){#x-ya-service-ticket-header}. 

Заголовок используется для авторизации вашего сервиса, если доступ к ЧЯ был выдан [для TVM-приложения и хостов](../concepts/getting-access.md#tvm-grants).

Для выписки Service-тикета рекомендуется пользоваться библиотекой [tvmauth](https://wiki.yandex-team.ru/passport/tvm2/library)
При запросе Service-тикета убедитесь, что в параметре `dst` запроса передается идентификатор приложения, соответствующий нужному вам [окружению ЧЯ](../concepts/location.md).
Идентификаторы для окружений ЧЯ перечислены в [таблице на Вики](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/#0-opredeljaemsjasokruzhenijami).

{% endcut %}
