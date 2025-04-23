---
title: Эксплуатация Travel-API
rank: 80
---

##  Эксплуатация Travel-API

Адрес балансера testing: `api.travel-balancer-test.yandex.net`
Адрес балансера prod: `api-prod.travel-hotels.yandex.net`

### Транк можно выкатить всегда

Новую функциональность можно убрать под флаги запроса. Нет известного конкретного (не теоретического) примера, когда была бы существенная необходимость заблокировать выкладку транка из-за проблем совместимости конкретно в API (иными словами: если нельзя выкатить API, то, скорее всего, нельзя выкатить и что-то еще).

### Автосборка

Используется отельная автосборка aka ПОНЯБот. Оповещения о сборке приходят в Slack, канал [#понябот-build-notifications](https://app.slack.com/client/T1B8NLW31/C7GNHMHJ9)

### Выкатка в тестинг

Происходит автоматически после успешной автосборки

### Выкатка в прод

Для выкатки нужно в [нашем CI](https://ci.travel-dev.yandex-team.ru/components) нажать `Release` у `API`

## Как откатить?
 [Инструкция](../../ops/tools/nanny.md#как-откатить-релиз).

## Послать запрос в тестинг

Запрос в тестинг можно послать через `curl` или [Swagger](https://api.travel-balancer-test.yandex.net/swagger-ui.html).
Понадобится сервисный тикет (`X-Ya-Service-Ticket`), получить который можно утилитой `$A/travel/hotels/tools/cli`.
Для работы утилиты нужно указать TVM секрет от приложения "CLI отелей": [Секрет в YAV](https://yav.yandex-team.ru/secret/sec-01dq7m5cccmhbgkeqt6pakj15k/).

```
cd $ARCADIA/travel/hotels/tools/cli
ya make
./hotels-cli --cli-tvm-secret={{secret}} ticket
```

### Запросы на ручку админки /api/admin/*

Для этого нам потребуется получить TVM Service ticket (заголовок `X-Ya-Service-Ticket`) тестовой админки и выписать себе TVM User Ticket (заголовок `X-Ya-User-Ticket`) от имени тестовой админки.

#### Получаем service ticket
Запрашиваем через
```
ya tool tvmknife get_service_ticket sshkey --src 2012628 --dst 2002548
```

Здесь `2012628` - это tvm id тестовой админки (travel-admin-testing);
`2002548` - это tvm id тестового travel-api (легаси название `API отелей (testing)`);

Полученный тикет сохраняем и затем будем подставлять в заголовок `X-Ya-Service-Ticket`.

<details>
<summary> Что делать если </summary>

#### нет прав TVM ssh user на сервис-источник

* Получить роль:

  https://wiki.yandex-team.ru/passport/tvm2/getabcrole/
  Название и ссылку ABC сервиса можно получить по tvm id так: `ya tool tvmknife info ...`

* Использовать секрет
  ```
  ya tool tvmknife get_service_ticket client_credentials --src 2012628 --dst 2002548 -S
  Enter secret: <tvm_travel_admin_testing_secret>
  ```
  Здесь `<tvm_travel_admin_testing_secret>` - секретный tvm ключ от тестовой админки ([найти в секретнице](https://yav.yandex-team.ru/secret/sec-01egt4zkze0fv34b2d93neadtt/explore/version/head)).
</details>

#### Получаем user ticket
Для начала нам нужен `oauth_token`. Для того чтобы его получить нужно выполнить
```
ya tool tvmknife get_user_ticket oauth --help
```
в выводе будут ссылки на получения токенов для разных инсталляций чёрного ящика.
Поскольку админка - это внутренний сервис, то и OAuth токен должен быть от внутреннего чёрного ящика (blackbox.yandex-team.ru)

Далее получаем user ticket от имени нужного сервиса (в нашем случае travel-admin-testing)
```
ya tool tvmknife get_user_ticket oauth -i 2012628 -b blackbox.yandex-team.ru
Enter 'token': <oauth_token>
```
Полученный тикет сохраняем и затем будем подставлять в заголовок `X-Ya-User-Ticket`.

Обратите внимание, что флаг `-b blackbox.yandex-team.ru` используется здесь только потому что мы ходим на ручки, которые
использует внутренний (staff) сервис. Для доступа к ручкам тестового внешнего api (travel-test.yandex.ru) использовать этот флаг не нужно (по умолчанию работает с тестовым внешним чёрным ящиком), 
но и OAuth токен нужно получать от внешнего ЧЯ.

Срок действия user ticket не более 5 минут, поэтому держите терминал открытым.

<details>
<summary> Что делать если </summary>

#### нет прав TVM ssh user на выбранный сервис

* Получить роль:

  https://wiki.yandex-team.ru/passport/tvm2/getabcrole/
  Название и ссылку ABC сервиса можно получить по tvm id так: `ya tool tvmknife info ...`

* Использовать секрет

  Например, для админки можно взять секрет tvm_travel_admin_testing_secret (ищи ссылку выше) и тогда команда на получение user ticket будет выглядить так:
```
ya tool tvmknife get_user_ticket oauth -i 2012628 -b blackbox.yandex-team.ru -S
Enter 'token': <oauth_token>
Enter 'secret':  <tvm_travel_admin_testing_secret>
```

#### выписанный тикет не подходит:
стоит проверить, через какой ЧЯ был получен user ticket. Дело может быть в том, что ручки админки работают с ЧЯ yandex-team, а не yandex.ru.
</details>

#### Ходим на ручки
Кроме `X-Ya-Service-Ticket` и `X-Ya-User-Ticket` ручки просят:

`X-Ya-YandexUid` - берём из одноименной куки `yandexuid` c домена `yandex-team.ru`

`X-Ya-PassportId` - можно взять из куки sessionid. Сама кука состоит из нескольких частей, разделенных вертикальной чертой `|`.
Пример: `3:blah-blah.hey-ney|PASSPORTID.other.stuff|doesnt.matter`.
По формуле `sessionid.split('|')[1].split('.')[0]` можно найти passportId.

Другой вариант - взять passportId из API паспорта. Для этого из залогиненого аккаунта нужно зайти по ссылке

| Окружение        | Ссылка                                           |
|------------------|--------------------------------------------------|
| yandex-team      | https://api.passport.yandex-team.ru/all_accounts |
| тестовый внешний | https://api.passport-test.yandex.ru/all_accounts |
| продовый внешний | https://api.passport.yandex.ru/all_accounts      |

Остальные заголовки, как правло опциональны.

Как быстрый вариант сходить в ручку на примере `/api/avia_booking_flow/v1/orders/state`
Заходим в заказ через инкогнито, вводим телефон из заказа - в таблице `authorized_users` появляется запись из нее берем `yandex_uid` и `session_key`

Полный пример вызова `api/admin/v1/list_orders`
```
BLACKBOX_YATEAM_OAUTH=<your oauth>
YANDEX_UID=<your yandex_uid>
PASSPORT_ID=<your passport_id>

TVM_SERVICE_TICKET=`ya tool tvmknife get_service_ticket sshkey --src 2012628 --dst 2002548`
TVM_USER_TICKET=`echo $BLACKBOX_YATEAM_OAUTH | ya tool tvmknife get_user_ticket oauth -i 2012628 -b blackbox.yandex-team.ru`

curl \
-H "Content-Type: application/json" \
-H "X-Ya-YandexUid: $YANDEX_UID" \
-H "X-Ya-Service-Ticket: $TVM_SERVICE_TICKET" \
-H "X-Ya-User-Ticket: $TVM_USER_TICKET" \
-H "X-Ya-PassportId: $PASSPORT_ID" \
-H "X-Ya-Login: monitorius" \
--data '{"order_state_filter": "OS_FULFILLED", "display_order_type_filter": "DT_HOTEL", "limit": 3}' \
"http://api.travel-balancer-test.yandex.net/api/admin/v1/list_orders"
```

