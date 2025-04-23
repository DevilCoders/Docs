## Примеры обращения к ручкам `/4.0/startup` и `/multiorderstate`

### Блок-схема работы бекенда

![stage-0](startup-stage-0.png)


### `/4.0/startup`


#### Возможные коды ответов:

- `200` - ok
- `401` - что-то не то с токеном, надо новый хороший. При этом клиент должен потереть токен и UserId
- `(401, 500)` - в кейсе прогрева делаем один запрос и не перезапрашиваем. Если пользователь кликнул на кнопку, то показываем соответствующие экраны. При антифроде показываем куда звонить. Иначе просто кнопку retry.
    - 403 - антифрод
    - 403 - отключено рубильником
- `500`: если лежит `launch` или `api-proxy`


#### Формат ответа при `401`

```json
{
  "code": "unauthorized",
  "message": "Not authorized request"
}
```


#### Формат ответа при `403`

Формат такой, как описано в [гайде](https://wiki.yandex-team.ru/taxi/backend/Taxi-API-Guide/#2.6.formatoshibok)

Для кода `blocked` тело ответа будет таким:

```json
{
  "code": "blocked",
  "message": "Вы заблокированы",
  "details": {
    "reason": "phone",
    "till": "2013-03-13T09:30:00+0000",
    "support_info": {
      "support_page": {
        "url": "https://m.taxi.yandex.ru/help"
      },
      "support_phone": "+7-499-705-88-88"
    }
  }
}
```

```json
{
  "code": "blocked",
  "message": "Что-то пошло не так"
}
```

Сейчас в `launch` информация о блокировании имеет такую структуру:

```json
"blocked": {
    "blocked": "2020-03-13T09:30:00+0000",
    "type": "phone"
}
```

Так как `startup` - это `4.0` ручка, формат будет другой.


#### Формат ответа при `200`

1\. Передаются token и user_id. Все валидно. Номер телефона тоже.

Параметры (`parameters`) берутся из экспериметра
[superapp_parameters_startup_ru](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/edit/superapp_parameters_startup_ru?type=experiments&name=superapp_pa)

```http
POST /4.0/startup
X-YaTaxi-UserId: c7e3c8c88f0dc8247196f11fe9df58e7
Authorization: Bearer AQAAAADvtHLOAAAIgerDQBbQVEi2qXMwUEDVnuQ

HTTP/1.1 200 OK
X-YaTaxi-UserId: c7e3c8c88f0dc8247196f11fe9df58e7
{
    "authorization_status": "authorized",
    "orders": [...],
    "parameters": {
      "eats": {
        "address_control_loading": "superapp_eats_address_control_loading",
        "address_control_title": "superapp_eats_address_control_title",
        "address_input_placeholder": "superapp_eats_address_input_placeholder",
        "address_search_on_map_header": "superapp_eats_address_search_on_map_header",
        "courier_max_distance_to_focus": 5000,
        "enabled": true,
        "mode": "eats",
        "service": "eats",
        "service_name": "superapp_eats_service_name",
        "title": "superapp_eats_card_title",
        "url": "https://tc.mobile.yandex.net/4.0/eda-superapp/",
        "user_agent_component": "Superapp/Eats"
      },
      "grocery": {
        "address_control_loading": "superapp_grocery_address_control_loading",
        "address_control_title": "superapp_grocery_address_control_title",
        "address_input_placeholder": "superapp_grocery_address_input_placeholder",
        "address_search_on_map_header": "superapp_grocery_address_search_on_map_header",
        "enabled": true,
        "mode": "grocery",
        "service": "grocery",
        "service_name": "superapp_grocery_service_name",
        "subtitle": "superapp_grocery_card_subtitle",
        "title": "superapp_grocery_card_title",
        "url": "https://tc.mobile.yandex.net/4.0/eda-superapp/restaurant/produkty_chamovniky",
        "user_agent_component": "Superapp/Grocery"
      },
      "l10n": {
        "superapp_eats_card_title": "Доставка из ресторанов",
        "superapp_eats_header_tag": "app_super_header_eats_ru",
        "superapp_eats_splash_tag": "app_super_splash_eats_ru",
        "superapp_eats_service_name": "Еда",
        "superapp_eats_card_subtitle": "до 15 мин",
        "superapp_grocery_card_title": ""
      },
      "tracking_api": "https://tc.mobile.yandex.net/4.0/eda-superapp/api/v2/orders/tracking",
      "support_info": {
        "support_page": {
          "url": "https://m.taxi.yandex.ru/help"
        },
        "support_phone": "+7-499-705-88-88"
      },
      "tracking_polling_interval": 600
    }
}
```

2\. Передаются token и user_id. Все валидно, кроме номера телефона.

Если у пользователя есть активные заказы, то `orders` в ответе будет даже при невалидном телефоне.
Если активных заказов нет, поля `orders` не будет.

```http
POST /4.0/startup
X-YaTaxi-UserId: c7e3c8c88f0dc8247196f11fe9df58e7
Authorization: Bearer AQAAAADvtHLOAAAIgerDQBbQVEi2qXMwUEDVnuQ

HTTP/1.1 200 OK
X-YaTaxi-UserId: c7e3c8c88f0dc8247196f11fe9df58e7
{
    "authorization_status": "phone_confirmation_required",
    "orders": []
    "parameters": {...}
}
```

3\. Если прийти без token и с z-user-id

> В STAGE-0 будет 401

```http
POST /4.0/startup
X-YaTaxi-UserId: z567e3c8c88f0dc8247196f11fe9df58e7

HTTP/1.1 200 OK
X-YaTaxi-UserId: z567e3c8c88f0dc8247196f11fe9df58e7
{
    "authorization_status": "unauthorized",
    "parameters": {...}
}
```

4\. Без token и с user_id (не Z)

> В STAGE-0 будет 401

```http
POST /4.0/startup
X-YaTaxi-UserId: c7e3c8c88f0dc8247196f11fe9df58e7

HTTP/1.1 200 OK
X-YaTaxi-UserId: z567e3c8c88f0dc8247196f11fe9df58e7
{
    "authorization_status": "unauthorized",
    "parameters": {...}
}
```

5\. Есть token, но он невалидный

```http
POST /4.0/startup
Authorization: Bearer AQAAAADvtHLOAAAIgerDQBbQVEi2qXMwUEDVnuQ

HTTP/1.1 401 Unauthorized
{
  "code": "unauthorized",
  "message": "Not authorized request"
}
```

6\. Нет ни токена, ни user_id

> В STAGE-0 будет 401

```http
POST /4.0/startup

HTTP/1.1 200 OK
X-YaTaxi-UserId: z567e3c8c88f0dc8247196f11fe9df58e7
{
    "authorization_status": "unauthorized",
    "parameters": {...}
}
```

7\. Все есть, но антифрод забанил пользователя

```http
POST /4.0/startup
Authorization: Bearer AQAAAADvtHLOAAAIgerDQBbQVEi2qXMwUEDVnuQ

HTTP/1.1 403 Forbidden
{
  "code": "blocked",
  "message": "Вы заблокированы",
  "details": {
    "reason": "phone",
    "till": "2013-03-13T09:30:00+0000",
    "support_info": {
      "support_page": {
        "url": "https://m.taxi.yandex.ru/help"
      },
      "support_phone": "+7-499-705-88-88"
    }
  }
}
```


### `/multiorderstate`

TODO: stage 2
