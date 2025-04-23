[Дизайн-ревью](https://wiki.yandex-team.ru/automotive/serverdevelopment/toll-roads-navi/design-review/)

## Клиент-серверное API
Общая структура ошибок для кода 422:
```json
{
    "code": "INVALID_PHONE_ID", // строковый ID ошибки
    "message": "Указанный номер телефона не найден", // текстовое описание
    // data - вспомогательные данные в зависимости от кода ошибки, опциональное поле
    "data": {
        "some_number": 42
    }
}
```

### Общий формат некоторых полей

* **price** - цена в копейках
* **car_plate** - госномер ТС, формат пока уточняется
* **vehicle_class_code** - класс ТС, в соответствии со спецификацией ЦКАД:
    - PASSENGER. Класс 1. Легковые транспортные средства. 1 ось и более.
    Высота до 2 метров. 
    - MEDIUM_SIZED. Класс 2. Среднегабаритные транспортные средства. 2 и более оси.
    Высота от 2 до 2.6 метров.
    - CARGO. Класс 3. Транспортные средства для перевозки грузов и автобусы. 2 оси.
    От 2.6 метров в высоту.
    - SPECIAL_CARGO. Класс 4. Специальные крупногабаритные транспортные средства и автобусы.
    3 и более осей. От 2.6 метров в высоту.

### Получение номера телефона пользователя
```
GET /tollroads/1.x/user/phone
Authorization: OAuth <токен>
```
**Ответ:**
```json
{
    "masked_phone": "+7 999 ***-**-33",
    "phone_id": "1234567890"
}
```
**401** - ошибки авторизации
**422** - другие ошибки
  * `code = PHONE_NOT_FOUND` - нет подтвержденного телефона в паспорте

### Получение стоимости проезда
```
POST /tollroads/1.x/route_price
Authorization: OAuth <токен>

{
  "vehicle_class_code": "PASSENGER",
  "plazas_array": [
    {
      "code": "plaza5018",
      "direction": "outer"
    },
    ...
  ]
}
```

В этом запросе поле **vehicle_class_code** опциональное. В случае, если его нет, бэкенд выдаёт минимальную цену проезда.

**Ответ:**
```json
{
  "price": 14000
}
```
**400** - невалидный json в запросе

### Оплата проезда
```
POST /tollroads/1.x/orders
Authorization: OAuth <токен>

{
  "car_plate": "x123xx750",
  "country_code": "RUS",
  "vehicle_class_code": "PASSENGER",
  "phone_id": "1234567890",
  "price": 14000,
  "plazas_array": [
    {
      "code": "plaza5018",
      "direction": "outer",
      "origin_point": {
        "lon": "56.127128",
        "lat": "37.898674"
      },
      "guide_point": {
        "lon": "56.127128",
        "lat": "37.898674"
       }
    },
    ...
  ]
}
```

Поле **country_code** — опциональное, по умолчанию считается "RUS".

**Ответ:**
```json
{
  "pay_token": "payment:gAAAAABeRd8t5MR3HZFQmUNm335isfaiqk0BnR9ajPxutTh-3ZO9w3taP-OeJiDG9cuKadIGQN3-eUd2pqVGDkMQXHubfzVusCBz8KOF3Dep7s6oihCqAb7tRogFgd2iw7YsXK-xyBR2gpdpJyEar2wxMK-fEn9AXAsUuXykZIk-eawM9nu8Rms=",
  "order_id": "42",
  "pay_id": "42"
}
```

**400** - невалидный json в запросе
**422** - другие ошибки
  * `code = INVALID_PRICE` - цена не совпала, в полях message и data будет передана актуальная цена.
    ```json
    {
        "code": "INVALID_PRICE",
        "message": "10000",
        "data": {
            "new_price": 10000
        }
    }
    ```
  * `code = INVALID_PHONE_ID` - phone_id не совпадает с тем, который возвращается в 
     методе `GET /carwashes/1.x/user/phone`

## Crowdtest

Для тестирования из Тулы, а также для асессоров сделан доступ через балансер Crowdtest.
Адрес балансера: `auto-navi-tollroads.crowdtest.yandex.ru`

Для доступа нужно:
- Получить в IDM роль "Qloud-окружения в Webauth / Qloud-ext / Maps / Auto-navi-tollroads / Пользователь"
- Получить OAuth-токен от yandex-team (сервис Webauth), пройдя по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=50136e798c0f440b864d606fcdb8d7b4).
  После редиректа в адресной строке в параметре `access_token` будет указан токен.
  (См. также [доки на OAuth](https://yandex.ru/dev/oauth/doc/dg/reference/mobile-client.html))

OAuth-токен от yandex-team надо указывать в заголовке `Webauth-Authorization`, например вот так:
```bash
curl https://auto-navi-tollroads.crowdtest.yandex.ru/tollroads/1.x/user/phone \
    -H 'Authorization: OAuth <...>' \
    -H 'Webauth-Authorization: OAuth <...>'
```

Также про работу с crowdtest и Webauth можно почитать:
- wiki:[Как пустить внешних асессоров в свою тестовую среду](https://wiki.yandex-team.ru/security/for/managers/kak-pustit-vneshnix-asessorov-v-svoju-testovuju-sredu/)
- wiki:[Двухфакторная аутентификация (TOTP) в интранете](https://wiki.yandex-team.ru/passport/yateamtotp/#dljaoutstaffsotrudnikiov/vneshnixkonsultantov)
  (нужно для асессоров)
- wiki:[Сервис Webauth](https://wiki.yandex-team.ru/intranet/webauth/)
- st:[VIEWER-775: WebAuth в Qloud](https://st.yandex-team.ru/VIEWER-775#5c87fb593a28d3001f284e6d)
- st:[QLOUDSUPPORT-4019: Некорректно работает PreAuthenticate](https://st.yandex-team.ru/QLOUDSUPPORT-4019#5d9c7de78c7003001d376d00)
- st:[MOBYANDEXIOS-8757: Сделать доработки для тестирования ПП на crowdtest-стендах](https://st.yandex-team.ru/MOBYANDEXIOS-8757)
- st:[MUSICANDROID-12621: Android. Сделать доработки для доступа в qa бэкенд с мобильных из внешней сети](https://st.yandex-team.ru/MUSICANDROID-12621)
