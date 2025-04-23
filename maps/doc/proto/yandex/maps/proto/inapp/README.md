Mobile clients
==============
Urls
----
**Environment** | **Url**
--|--
testing | http://core-inapp-transport.common.testing.maps.yandex.net
stable | http://core-inapp-transport.maps.yandex.net


Commmon id parameters
------------------
**Parameter** | **Meaning** | **Example**
--|--|--
miid | library installation id | `miid=bee97ee80fc69520dd5309cfa5a734a355e9489bf`
deviceid | metrika device id | `deviceid=89662b18fd46f33c21728a5d0425b0bf`
uuid | metrika user id | `uuid=99519f6025935c9a8c546bda0fc959c6`

/v1/messages (GET)
---------
Получить список сообщений для этого пользователя
Method |  GET
--|--
**Params** | common id parameters
**Request headers**  |
 *If-None-Match* | `If-None-Match: W/"c54bf4ceec5fb8c9b89d9d242393f3bc"`
 *X-Ya-User-Ticket* | `X-Ya-User-Ticket: 3:user:DIN1EMaW3vw...`
**Response** | [MessageList](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/inapp/service.proto#L18)
**Response headers**|
 *Content-Type* |  `Content-Type: application/x-protobuf`
 *Etag* |  `Etag: W/"c54bf4ceec5fb8c9b89d9d242393f3bc"`
**Response codes**| 200, 304, 429


/v1/interact (POST)
---------
Отправить взаимодействия пользователя с сообщениями

Method |  POST
--|--
**Params** | common id parameters
**Request body**|[InteractionList](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/inapp/service.proto#L23)
**Request headers**|
*X-Ya-User-Ticket* | `X-Ya-User-Ticket: 3:user:DIN1EMaW3vw...`
**Response** | empty

HTTP response code | Meaning
--|--
200 | ok
429, 5xx | повторите попытку позже

Backoffice
==========

Urls
----
**Environment** | **Url**
--|--
testing | http://core-inapp-backoffice.common.testing.maps.yandex.net
stable | http://core-inapp-backoffice.maps.yandex.net

/v1/send (POST)
------------
Послать сообщения одному или нескольким пользователям

Method | POST
--|--
**Request**| [SendData](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/inapp/backoffice.proto#L14)
**Response** | empty

Request header| Example | Details
--|--|--
*X-Ya-Service-Ticket* | `X-Ya-Service-Ticket: 3:serv:EJN3FMbW4d2...` | required, should correspond to `sender`||

Parameter | Example | Details
--|--|--
message_id | `message_id=90d65c90fb087173` | required
sender | `sender=geoadv` | required
priority | `priority=10` | optional, default: 0
deliver_at | `deliver_at=1603464252` | UTC timestamp, optional, default: at once ||
ttl | `ttl=86400` | in seconds, default: 604800 (a week) |
ttl_after_read | `ttl_after_read=3600` | optional, default: not set |

HTTP response code | Meaning
--|--
200 | сообщения приняты для доставки
400 | во входных параметрах что-то не так
429 | слишком много сообщений от данного `sender`, повторите попытку позже
