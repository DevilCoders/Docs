# Заголовки отправляемые во все бекенды

Во все бекенды из ноды, при использовании HttpClient, отправляются следующие заголовки:

-   X-Ya-User-Ticket
-   X-Ya-YandexUid
-   X-Ya-PassportId
-   X-Ya-Login
-   X-Ya-Session-Key
-   X-Request-Id
-   X-Ya-Uaas-Experiments
-   X-Ya-User-Ip

Для бекендов требующих _service ticket_ также отправляется заголовок `X-Ya-Service-Ticket`

## Заголовки, которые присутствуют во всех запросах

-   X-Ya-YandexUid - идентификатор, который привязывается к конкретному устройству пользователя на домене `.yandex.{tld}`
-   X-Request-Id - идентификатор запроса
-   X-Ya-Uaas-Experiments - объект экспериментов куда попал текущий пользователь: `{"ключ эксперимента": "значение эксперимента"}`, сериализованный в JSON. Подробнее [тут](https://nda.ya.ru/3VDWEM)
-   X-Ya-Session-Key - идентификатор, который привязывается к конкретному устройству пользователя на домене `travel.yandex.{tld}`
-   X-Ya-User-Ip - Ip адрес пользователя

## Заголовки, которые присутствуют если пользователь залогинен

-   X-Ya-User-Ticket - user ticket
-   X-Ya-PassportId - идентификатор пользователя
-   X-Ya-Login - логин пользователя

Что такое _service ticket_ и _user ticket_ можно почитать [тут](https://ui.yandex-team.ru/core/tvm)
