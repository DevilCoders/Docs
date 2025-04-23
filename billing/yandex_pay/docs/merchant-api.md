# Merchant API

Интеграция Yandex Pay Checkout состоит из нескольких частей:

- установка кнопки Yandex Pay Checkout на фронте продавца;
- разработка взаимодействия между бэкендами продавца и Yandex Pay;
- настройка параметров шлюза в [консоли Yandex Pay](https://console.pay.yandex.ru).

Для установки кнопки на сайте необходимо следовать [документации для фронтенда](https://pay.yandex.ru/ru/docs/tutorial/yandex-pay-checkout).

Данный документ определяет схему взаимодействия между бэкендом Yandex Pay и бэкендом продавца. Взаимодействие строится на двух API:

- Yandex Pay -> Merchant API: запросы из бэкенда Yandex Pay в бэкенд продавца для получения данных по корзине и создания заказа.
- Merchant -> Yandex Pay API: запросы из бэкенда продавца в бэкенд Yandex Pay для управления заказом.

## Схема взаимодействия между продавцом и Yandex Pay

![Схема взаимодействия](./overview.svg "Создание заказа")

1. Покупатель нажимает кнопку Yandex Pay Checkout.
2. Yandex Pay идет с запросом на получение деталей по корзине к продавцу в `/order/render`.
3. На основе данных продавца и персональных данных пользователя Yandex Pay отображает форму оформления заказа.
4. Покупатель выбирает способ доставки и инициирует оплату.
5. Yandex Pay авторизовывает (запрашивает разрешение на оплату) заказ на стороне продавца через вызов `/order/create`.
6. Продавец проверяет детали заказа, резервирует товар и разрешает оплату.
7. Yandex Pay проводит платеж через платежный шлюз продавца.
8. Yandex Pay уведомляет продавца о статусе платежа через вызов `/webhook`.
9. Покупатель видит статус оплаты и закрывает форму.

Покупатель перед оплатой может вносить изменения на форму: изменять адрес доставки, вводить купон на скидку. После каждого изменения бэкенд Yandex Pay будет повторять шаги 2-3.

Продавец может управлять заказом через Merchant -> Yandex Pay API: списывать средства для двухстадийных платежей, выполнять возврат и прочее.

## План интеграции Yandex Pay Checkout

1. Зарегистрируйте `merchant_id` в Yandex Pay Sandbox. Настройте адрес вашего бэкенда через Yandex Pay Console.
2. Выполните интеграцию кнопки на фронте. Установите окружение `Sandbox` в параметрах кнопки.
3. Реализуйте обработку запросов Yandex -> Merchant API. После реализации данного шага можно создать тестовый заказ.
4. Опционально реализуйте вызовы Merchant -> Yandex Pay API для управления заказом из бэкофиса продавца.

## Использование Yandex Pay Checkout для оплаты оформленного заказа

Кнопка Yandex Pay может располагаться на форме оплаты оформленного заказа стандартным способом продавца. Для данного случая необходимо включить изменения:

- в ответе `/order/render` не требовать контакты и адрес доставки
- на фронте передать идентификатор уже созданного заказа через `orderId`.

В запросе `/order/render` бэкенд продавца получит идентификатор заказа продавца. По данному признаку бэкенд должен вернуть метаданные созданного заказа.

## Яндекс Доставка в Yandex Pay Checkout

Для того чтобы опции Яндекс Доставки отобразились пользователю на форме Yandex Pay Checkout, необходимо:
1. В [консоли Yandex Pay](https://console.pay.yandex.ru) включить интеграцию.
2. Вернуть в ответе `/order/render` необходимые даннные:
   - в `shipping.availableMethods` должен присутствовать `YANDEX_DELIVERY`
   - для каждого товара в корзине указать его размеры
   - в `shipping.yandexDelivery.warehouse` заполнить информацию о складе, откуда курьер сможет забрать заказ

Механика работы Доставки:
1. Пользователь при оформлении выбирает опцию Яндекс Доставки.
2. Yandex Pay проводит авторизацию платежа за заказ.
3. Магазин собирает заказ и инициирует доставку запросом `/delivery/create`.
4. Яндекс Доставка оценивает стоимость, и после завершения оценки доставка переходит в статус `READY_FOR_APPROVAL`.
5. Магазин подтверждает доставку запросом `/delivery/accept` в течение 10 минут после завершения оценки.
   - Если прошло более 10 минут, доставка переходит в статус `EXPIRED`.
   - Магазин может обновить доставку запросом `/delivery/renew` и вернуться к пункту 4.
6. Запускается процесс доставки заказа покупателю:
   - Служба доставки получает заказ от продавца.
   - Служба доставки отвозит заказ получателю.
   - Если не удалось вручить заказ получателю, он возвращается обратно.
7. Yandex Pay уведомляет продавца об изменении статусов доставки через вызов `/webhook`.
8. Магазин может отменить доставку платно или бесплатно в зависимости от текущего статуса запросом `/delivery/cancel`.
   - Информация о возможности отмены (платно, бесплатно, недоступно) доступна в ответе `/delivery/cancel-info`.

При включенном Автоподтверждении пункты 3 и 5 Yandex Pay выполнит автоматически сразу после успешной авторизации платежа.

## Yandex Pay -> Merchant API

### Аутентификация запроса Yandex Pay

В теле запроса Yandex Pay присылает JWT-токен, подписанный по алгоритму ES256. Токен состоит из трех частей: заголовка (header), полезной нагрузки (payload) и подписи, конкатенированных через точку: `<base64-encoded headers JSON>.<base64-encoded payload JSON>.<signature>` Раскодированный из base64 заголовок представляет собой JSON документ со следующей структурой:

```json
{
  "alg": "ES256",         // алгоритм подписи
  "kid": "key-id",        // ID ключа, используется при определении публичного ключа
  "iat": "1639408318",    // UNIX время, когда токен был выпущен
  "exp": "1639429918",    // UNIX время, когда токен истекает, токен признается не валидным после наступления этого времени
  "typ": "JWT"            // тип токена
}
```

Полезная нагрузка также представляет собой JSON, конкретная структура полей которого определяется вызываемым методом (см. "Методы" ниже). Подпись необходима для проверки валидности JWT токена. **Важно:** перед десериализацией токена необходимо проверить его валидность.

#### Алгоритм проверки валидности токена

Для проверки валидности JWT-токена рекомендуем воспользоваться одной из стандартных библиотек из списка: <https://jwt.io/libraries> и по возможности воздержаться от ручной реализации данных проверок.

В общем случае, алгоритм проверки JWT-токена с помощью библиотеки включает в себя:

1. Проверку валидности подписи JWT-токена с помощью публичных JWK-ключей, размещенных по адресам: <https://sandbox.pay.yandex.ru/api/jwks> для тестового окружения и <https://pay.yandex.ru/api/jwks> для продуктивного окружения. Публичный ключ, используемый для валидации подписи конкретного JWT-токена, выбирается на основе требований `alg` и `kid` в заголовке самого токена.
2. Проверку стандартных требований в заголовках JWT-токена: `alg`, `typ`, `iat`, `exp` и т.д.

Только в случае, если обе проверки прошли успешно, получатель может десериализовать JSON payload JWT токена. После этого получатель должен дополнительно проверить, что `merchantId` в payload токена совпадает с ID продавца в Yandex Pay; токен не может быть использован в противном случае.

Если любая из проверок завершилась неуспехом, токен считается невалидным, запрос считается неаутентифицированным и должен быть отклонен. В этом случае ожидается ответ `403 Forbidden` со следующей схемой тела ответа:

```jsonc
{
    "code": 403,
    "reasonCode": "FORBIDDEN",  # код ошибки
    "reason": string or null    # текстовое описание ошибки, например: "Invalid merchantId"
}
```

#### Кэширование публичных JWK-ключей

Допускается кэширование JWK-ключей, используемых для валидации JWT-токенов, на бэкенде продавца. Время жизни такого кэша необходимо устанавливать таким образом, чтобы это не приводило к ошибкам валидации токенов в случае ротации JWK-ключей на стороне Yandex Pay. На практике [некоторые библиотеки](https://github.com/auth0/node-jwks-rsa#caching) по умолчанию устанавливают время жизни такого кэша в 10 минут. В случае кэширования JWK-ключей, необходимо реализовать следующие сценарии проверок.

Сценарий А: Успешная валидация токена кэшированными JWK-ключами.

1. Приходит запрос с токеном, чей `kid` найден среди кэшированных JWK-ключей, и время жизни кэша не истекло.
2. Валидация подписи токена завершается успешно.
3. Токен считается валидным.

Сценарий B: Неуспешная валидация токена кэшированными JWK-ключами.

1. Приходит запрос с токеном, чей `kid` найден среди кэшированных JWK-ключей, и время жизни кэша не истекло.
2. Валидация подписи токена завершается неуспехом.
3. Токен считается невалидным, запрос отклоняется.

Сценарий C: Валидация токена со сбросом кэша JWK-ключей.

1. Приходит запрос с токеном, чей `kid` не найден среди кэшированных JWK-ключей **или** время жизни кэша истекло.
2. Продавец должен сбросить кэш JWK-ключей и запросить весь список активных JWK-ключей заново с соответствующего окружению адреса.
3. Валидация продолжается по сценарию А или B.

Как и в случае с валидацией токена, рекомендуется использовать стандартные библиотеки и воздержаться от ручной реализации данных сценариев.

#### Пример валидации JWT токена на Python

Ниже приведен пример успешной валидации JWT токена, выпущенного в sandbox окружении.
Для валидации токенов в продакшен окружении должны использоваться публичные ключи, доступные по адресу <https://pay.yandex.ru/api/jwks>

```python
import json
from urllib.request import urlopen
from jose import jwt


YANDEX_JWK_ENDPOINT = "https://sandbox.pay.yandex.ru/api/jwks"

JWT_TOKEN = (
"eyJhbGciOiJFUzI1NiIsImlhdCI6MTY1MDE5Njc1OCwia2lkIjoidGVzdC1rZXkiLCJ0eXAiOiJKV1QifQ.eyJjYXJ0Ijp7Iml0ZW1zIjpbeyJwcm9kdWN"
"0SWQiOiJwMSIsInF1YW50aXR5Ijp7ImNvdW50IjoiMSJ9fV19LCJjdXJyZW5jeUNvZGUiOiJSVUIiLCJtZXJjaGFudElkIjoiMjc2Y2YxZjEtZjhlZC00N"
"GZlLTg5ZTMtNWU0MTEzNDZkYThkIn0.YmQjHlh3ddLWgBexQ3QrwtbgAA3u1TVnBl1qnfMIvToBwinH3uH92KGB15m4NAQXdz5nhkjPZZu7RUStJt40PQ"
)

with urlopen(YANDEX_JWK_ENDPOINT) as response:
    public_jwks = json.load(response)

payload = jwt.decode(JWT_TOKEN, public_jwks, algorithms=["ES256"])
print(json.dumps(payload, indent=2))

# {
#   "cart": {
#     "items": [
#       {
#         "productId": "p1",
#         "quantity": {
#           "count": "1"
#         }
#       }
#     ]
#   },
#   "currencyCode": "RUB",
#   "merchantId": "276cf1f1-f8ed-44fe-89e3-5e411346da8d"
# }
```

### API вызовы со стороны Yandex Pay в бэкенд продавца

#### Запрос информации для отображения корзины

`POST <base_url>/v1/order/render`

На входе идентификаторы товаров и их количество.
Имеется возможность передать произвольные данные в поле `metadata` с фронтенда продавца на бэкенд продавца.
Метод вызывается при изменении состава корзины, выборе адреса, способа доставки, вводе промо-кодов.
Продавцу необходимо проверять состав заказа и заполнять детальную информацию для товаров, способов доставки и промо-кодов,
пересчитывать стоимости товаров и всего заказа.

В ответе ожидаются детальная информация по заказу и товарам:

- Доступные типы способов доставки и оплаты в `availablePaymentMethods`, `shipping.availableMethods`
- Дополнительные данные пользователя необходимые для оформления заказа, в `requiredFields`
- Стоимость каждого товара и название. Опционально, максимально доступное количество товара
- Информация о скидках, применённых к корзине, в `discounts`

Тело запроса (payload JWT-токена):

```jsonc
{
    "merchantId": uuid,
    "currencyCode": string,              # Валюта заказа (ISO 4217)
    "orderId": string,                   # Опционально. Id существующего заказа на стороне продавца,
                                         # переданный при инициализации кнопки
    "cart": {
        "cartId": string,                # Внутренний id Yandex Pay
        "externalId": string or null,    # Id корзины в системе продавца, если был передан при инициализации кнопки
        "items": array<{
            "productId": string,         # Id товара в системе продавца
            "quantity": {                # Опционально. Количество товара в заказе
                "count": decimal ("42.00")
            }
        }>,

        "coupons": array<{   # Опционально. Применённые скидочные купоны
            "value": string
        }>,
    },

    "shippingAddress": {  # Опционально. Адрес доставки
        "country": string,
        "region": string or null,
        "regionHierarchy": [ ... ],
        "locality": string,
        "district": string or null,
        "street": string or null,
        "building": string,
        "room": string or null,
        "entrance": string or null,
        "floor": string or null,
        "intercom": string or null,
        "zip": string or null,
        "locale": string or null,
        "comment": string or null,
        "addressLine": string or null,  # Полный адрес
        "location": {  # optional
            "longitude": number,
            "latitude": number
        }
    },

    "metadata": string or null  # Произвольные данные, переданные при инициализации кнопки
}
```

Ответ:

- В случае успеха ожидается ответ `200 OK` и актуальная корзина с методами доставки:

```jsonc
{
    "status": "success",
    "data": {
        "currencyCode": string,
        "availablePaymentMethods": array<enum<CARD|SPLIT|CASH_ON_DELIVERY|CARD_ON_DELIVERY>>,
        "enableCoupons": boolean,
        "enableCommentField": boolean,

        "requiredFields": {             # Данные пользователя, необходимые для оформления заказа
            "billingContact": {
                "name": boolean,
                "email": boolean
            },
            "shippingContact": {
                "name": boolean,
                "email": boolean,
                "phone": boolean
            },
        },

        "cart": {
            "items": array<{
                "type": enum<PHYSICAL|DIGITAL|UNSPECIFIED>,  # Тип товара. Важен для интеграции с доставками
                "productId": string,
                "unitPrice": decimal ("42.00"),           # Полная цена за единицу товара
                "discountedUnitPrice": decimal ("42.00"), # Цена за единицу товара с учетом скидки
                "subtotal": decimal ("42.00"),            # Суммарная цена за позицию без учета скидок
                "total": decimal ("40.00"),               # Суммарная цена за позицию со всеми скидками
                "title": string,                          # Название товара
                "receipt": {...},                         # Опционально. Данные для формирования чека
                "quantity": {
                    "count": decimal ("42.00"),           # Количество товара в заказе
                    "available": decimal ("42.00"),       # Максимально доступное количество товара
                    "label": string                       # Опционально. Название единиц измерения, например "кг" или "шт.".
                },

                "measurements": {          # Опционально. Размеры и вес товара. Обязательно для товаров типа PHYSICAL
                    "weight": number,      # Вес товара в килограммах.

                    "height": number,      # Размеры в метрах.
                    "length": number,
                    "width": number
                }
            }>,

            "coupons": array<{
                "value": string,                # Код купона.
                "status": enum<VALID|INVALID|EXPIRED>,
                "description": string           # Например, "Скидка 3%"
            }>,

            "discounts": array<{                # Опционально. Скидки, применённые к корзине
                "discountId": string,
                "amount": decimal ("42.00"),    # Сумма скидки
                "description": string           # Текстовое описание
            }>,

            "total": {                          # Суммарная стоимость корзины (без учёта доставки)
                "amount": decimal ("42.00"),
                "label": string or null
            },

            "measurements": {          # Опционально. Размеры и вес корзины.
                "weight": number,

                "height": number,
                "length": number,
                "width": number
            }
        },

        "shipping": {
            "availableMethods": array<enum<COURIER|PICKUP|YANDEX_DELIVERY>>,

            "availableCourierOptions": array<{   # Скорректированные варианты доставки (при наличии адреса в запросе)
                "courierOptionId": string,
                "provider": enum<COURIER|CDEK|EMS|DHL|RUSSIAN_POST|BOXBERRY>,   # Идентификатор службы доставки.
                "category": enum<EXPRESS|TODAY|STANDARD>,
                "title": string,            # Название способа доставки
                "amount": decimal ("42.00"),
                "receipt": {...},           # Опционально. Данные для формирования чека
                "fromDate": string,         # YYYY-MM-DD. Ближайшая возможная дата доставки
                "toDate": string,           # Опционально. YYYY-MM-DD. Самая поздняя дата доставки
                "fromTime": string,         # Опционально. HH:mm. Начало интервала времени доставки.
                "toTime": string,           # Опционально. HH:mm. Конец интервала времени доставки.

                # Опционально. Доступные методы оплаты заказа при выбранном способе доставки
                "allowedPaymentMethods": array<enum<CARD|SPLIT|CASH_ON_DELIVERY|CARD_ON_DELIVERY>>,
            }>,
            # Опционально. Если используется интеграция с Яндекс Доставкой
            "yandexDelivery": {
                "warehouse": {
                    "contact": {
                        "firstName": string or null,
                        "secondName": string or null,
                        "lastName": string or null,
                        "email": string or null,
                        "phone": string or null
                    },
                    "emergencyContact": {
                        "firstName": string or null,
                        "secondName": string or null,
                        "lastName": string or null,
                        "email": string or null,
                        "phone": string or null
                    },
                    "address": {
                        "country": string,
                        "region": string or null,
                        "locality": string,
                        "district": string or null,
                        "street": string or null,
                        "building": string,
                        "room": string or null,
                        "entrance": string or null,
                        "floor": string or null,
                        "intercom": string or null,
                        "zip": string or null,
                        "locale": string or null,
                        "comment": string or null,
                        "addressLine": string or null,  # Полный адрес
                        "location": {  # optional
                            "longitude": number,
                            "latitude": number
                        }
                    }
                }
            }
        },

        "metadata": string or null
    }
}
```

- В случае некорректного заказа ожидаем `400 Bad Request` со следующей схемой тела ответа:

```jsonc
{
    "status": "fail",
    "reasonCode": string,     # код ошибки (см. список возможных кодов ниже)
    "reason": string or null  # текстовое описание ошибки, например: "order error: ..."
}
```

| reasonCode         | Описание                                     |
|--------------------|----------------------------------------------|
| `OUT_OF_INVENTORY` | Товар более недоступен в заданном количестве |
| `ITEM_NOT_FOUND`   | Товар с указанным идентификатором не найден  |
| `OTHER`            | Иные причины                                 |

#### Валидация и создание заказа на стороне продавца (/order/create)

В параметрах запроса передаётся заполненная корзина с ценами товаров, выбранным способом доставки и полной ценой заказа (`orderAmount`). Продавец проверяет корректность цен и состава корзины.

Если корзина корректна, то продавец резервирует товар на 30 минут и отвечает успешным кодом ответа в бэкенд Yandex Pay. Бэкенд Yandex Pay в течении 30 минут должен прислать нотификации о статусе оплаты. Так же продавец может poll-ить статус заказа через ручку получения деталей заказа в Merchant -> Yandex Pay API.

Если в течении 30 минут заказ не был оплачен, то продавец может снимать резерв с товаров и отмечать заказ отменённым.

`POST <base_url>/v1/order/create`

Тело запроса (payload JWT-токена):

```jsonc
{
    "merchantId": uuid,
    "currencyCode": string,    # Валюта заказа (ISO 4217)
    "orderId": string,         # Опционально. Id существующего заказа на стороне продавца, переданный при инициализации кнопки
    "cart": {
        "cartId": string,      # Внутренний id Yandex Pay
        "externalId": string,  # Опционально. Переданный продавцом Id заказа.
        "total": {
            "amount": decimal ("322.00"), # Стоимость корзины без учета доставки.
            "label": string or null
        },
        "items": array<{  # optional
            "productId": string,          # Id товара в системе продавца
            "total": decimal ("42.00"),
            "title": string,
            "quantity": {  # optional
                "count": decimal ("42.00"),
                "label": string or null
            }
        }>,

        "comment": string or null,   # Комментарий пользователя к заказу
        "coupons": array<{           # Опционально. Скидочные купоны
            "value": string
        }>,

        "discounts": array<{                # Опционально. Скидки, применённые к корзине.
            "discountId": string,
            "amount": decimal ("42.00"),    # Сумма скидки
            "description": string           # Текстовое описание
        }>,
    },

    "billingContact": {  # optional
        "firstName": string or null,
        "secondName": string or null,
        "lastName": string or null,
        "email": string or null,
        "phone": string or null
    },

    "shippingContact": {  # optional
        "firstName": string or null,
        "secondName": string or null,
        "lastName": string or null,
        "email": string or null,
        "phone": string or null
    },

    "shippingAddress": { # Адрес доставки доступен, если выбран метод COURIER.
        "country": string,
        "region": string or null,
        "locality": string,
        "district": string or null,
        "street": string or null,
        "building": string,
        "room": string or null,
        "entrance": string or null,
        "floor": string or null,
        "intercom": string or null,
        "zip": string or null,
        "locale": string or null,
        "comment": string or null,
        "addressLine": string or null,  # Полный адрес
        "location": {  # optional
            "longitude": number,
            "latitude": number
        }
    },

    "orderAmount": decimal ("350.00"),  # Полная стоимость заказа к оплате с учётом доставки, скидок и промокодов.

    "paymentMethod": {  # Выбранный способ оплаты
        "methodType": enum<CARD|SPLIT|CASH_ON_DELIVERY|CARD_ON_DELIVERY>,
        "cardLast4": string,
        "cardNetwork": enum<VISA|MASTERCARD|MIR|...>,  # Платежная система.
    },

    "shippingMethod": {  # Выбранный способ доставки
        "methodType": enum<COURIER|PICKUP|YANDEX_DELIVERY>,

        "courierOption": {  # если methodType == COURIER
            "courierOptionId": string,  # id выбранного варианта доставки в системе продавца.
            "amount": decimal ("42.00"),
            "provider": string,
            ...
        },

        "pickupOption": {  # если methodType == PICKUP
            "pickupPointId": string,  # идентификатор точки самовывоза
            "amount": decimal ("42.00"),
            ... # прочие детали выбранного способа
        },

        "yandexDeliveryOption": {  # если methodType == YANDEX_DELIVERY
            "yandexDeliveryOptionId": string, # Id предложения Яндекс Доставки
            "amount": decimal ("22"), # Стоимость доставки
            ... # прочие детали выбранного способа
        }
    },

    "metadata": string or null  # Произвольные данные, переданные при инициализации кнопки
}
```

Ответ:

- В случае валидного заказа ожидаем `200 OK` и тело:

    ```json
    {
        "status": "success",
        "data": {
            "orderId": string,  # ID созданного заказа на стороне продавца.
            "metadata": string or null
        }
    }
    ```

- В случае неуспешной валидации ожидаем `400 Bad Request` со следующей схемой тела ответа:

    ```json
    {
        "status": "fail",
        "reasonCode": string,     # код ошибки (см. список возможных кодов ниже)
        "reason": string or null  # текстовое описание ошибки, например: "order error: ..."
    }
    ```

| reasonCode                  | Описание                                              |
|-----------------------------|-------------------------------------------------------|
| `ORDER_AMOUNT_MISMATCH`     | Несоответствие суммы заказа данным продавца           |
| `ORDER_DETAILS_MISMATCH`    | Несоответствие иных параметров заказа данным продавца |
| `SHIPPING_DETAILS_MISMATCH` | Несоответствие параметров доставки данным продавца    |
| `OTHER`                     | Иные причины                                          |

В случае получения 4xx ответа валидация заказа считается неуспешной,
оплата заказа не будет проводиться, повторных попыток проверки заказа осуществляться не будет.
В случае получения 5xx ответа запрос будет повторён.

#### Нотификации об изменении статуса

`POST <base_url>/v1/webhook`

Поддерживаемые события:

- `ORDER_STATUS_UPDATED` - изменение статуса платежа или доставки
- `OPERATION_STATUS_UPDATED` - изменение статуса операции по подтверждению, отмене или возврату платежа

Тело запроса (payload JWT-токена):

```jsonc
{
    "merchantId": uuid,
    "event": enum<ORDER_STATUS_UPDATED|OPERATION_STATUS_UPDATED>,
    "eventTime": string           # время события в формате `RFC 3339`; `YYYY-MM-DDThh:mm:ssTZD`
    "order": {                    # если event == ORDER_STATUS_UPDATED
        "orderId": string,        # id заказа, пришедший в ответе /order/create
        "paymentStatus": enum<>,  # Опционально. Статус заказа (см. список возможных статусов ниже).
        "deliveryStatus": enum<>, # Опционально. Статусы доставки (см. список возможных статусов ниже).
    },
    "operation": {                # если event == OPERATION_STATUS_UPDATED
        "operationId": string,
        "orderId": string,
        "externalOperationId": string or null,
        "operationType": enum<AUTHORIZE|REFUND|CAPTURE|VOID>,
        "status": "FAIL",
    }
}
```

В случае оплаты при получении (`CASH_ON_DELIVERY` или `CARD_ON_DELIVERY`) нотификации об изменении статуса не отправляются.

**Важно:** `data.orderId` должен совпадать с идентификатором имеющегося у продавца заказа.

Возможные статусы оплаты:

| Статус               | Описание                                                                  |
|----------------------|---------------------------------------------------------------------------|
| `PENDING`            | Ожидается оплата.                                                         |
| `AUTHORIZED`         | Платеж за заказ авторизован. Средства заблокированы на счету плательщика. |
| `CAPTURED`           | Заказ успешно оплачен. Средства списаны со счета плательщика.             |
| `VOIDED`             | Оплата отменена (voided). Списание средств не производилось.              |
| `REFUNDED`           | Совершён возврат средств за заказ                                         |
| `PARTIALLY_REFUNDED` | Совершён частичный возврат средств за заказ                               |
| `FAILED`             | Заказ не был успешно оплачен.                                             |


Возможные статусы доставки:

| Статус               | Описание                                                   |
|----------------------|------------------------------------------------------------|
| `ESTIMATING`         | Идет вычисление стоимости доставки                         |
| `EXPIRED`            | Доставка не подтверждена за отведенное время               |
| `READY_FOR_APPROVAL` | Доставка ждет подтверждения                                |
| `COLLECTING`         | Идет процесс получения заказа службой доставки от продавца |
| `PREPARING`          | Идет подготовка к отправке покупателю                      |
| `DELIVERING`         | Заказ доставляется покупателю                              |
| `DELIVERED`          | Заказ доставлен                                            |
| `RETURNING`          | Заказ возвращается обратно продавцу                        |
| `RETURNED`           | Заказ возвращен продавцу                                   |
| `FAILED`             | Доставка завершилась ошибкой                               |
| `CANCELLED`          | Доставка отменена продавцом                                |

Ответ:

- В случае успешной обработки нотификации ожидаем `200 OK` и тело:

    ```json
    {
        "status": "success"
    }
    ```

- В случае неуспешной валидации ожидаем `400 Bad Request` со следующей схемой тела ответа:

    ```json
    {
        "status": "fail",
        "reasonCode": string,     # код ошибки (см. список возможных кодов ниже)
        "reason": string or null  # текстовое описание ошибки, например: "order not found"
    }
    ```

| reasonCode        | Описание        |
|-------------------|-----------------|
| `ORDER_NOT_FOUND` | Заказ не найден |
| `OTHER`           | Иные причины    |

В случае получения 4xx или 5xx ответа запрос будет повторён.

#### Получение точек самовывоза

`POST <base_url>/v1/pickup-options`

В ответе на запрос может отсутствовать стоимость и время доставки в точку самовывоза.
При клике по точке самовывоза на форме Yandex Pay запросит детали доставки через `pickup-option-details`.

Тело запроса (payload JWT-токена):

```jsonc
{
    "merchantId": uuid,
    "currencyCode": string,
    "cart": {                   # Корзина c ценами, размером и весом товаров.
        "cartId": "string",
        "externalId": string,   # Опционально. Id корзины в системе продавца.
        "items": array<{
            "productId": string,
            "quantity": {
                "count": decimal ("42.00")
            }
        }>,
        "coupons": array<{
            "value": string
        }>
    },
    "metadata": string or null,

    "boundingBox": {            # Границы области на карте
        "sw": {                 # Левый нижний угол (юго-запад)
          "latitude": number,
          "longitude": number
        },
        "ne": {                 # Правый верхний угол (северо-восток)
          "latitude": number,
          "longitude": number
        }
    }
}
```

Ответ:

- В случае успеха ожидаем `200 OK` и точки самовывоза:

```jsonc
{
    "status": "success",
    "data": {
        "pickupOptions": array<{
            "pickupPointId": string,            # Уникальный id точки самовывоза в системе продавца
            "title": string,                    # Название точки самовывоза
            "address": string,                  # Адрес в виде строки
            "provider": enum<PICKPOINT|...|IN_STORE>,
            "location": {
                "longitude": number,
                "latitude": number
            },

            "amount": decimal ("42.00"),        # Опционально. Стоимость доставки в точку

            "fromDate": string,                 # YYYY-MM-DD. Ближайшая возможная дата доставки
            "toDate": string,                   # Опционально. YYYY-MM-DD. Самая поздняя дата доставки

            "description": string or null,      # Опционально. Дополнительное описание
            "phones": array<string> or null,    # Опционально. Телефоны для связи

            "schedule": [                       # Опционально. График работы точки.
                {
                    "label": string,            # Например, "пн-пт"
                    "fromTime": string,         # HH:mm, "08:00"
                    "toTime": string,           # HH:mm, "20:00"
                }
            ],

            "storagePeriod": int,               # Опционально. Срок хранения товара в точке самовывоза в днях.

            # Опционально. Доступные методы оплаты заказа при выбранном способе самовывоза
            "allowedPaymentMethods": array<enum<CARD|SPLIT|CASH_ON_DELIVERY|CARD_ON_DELIVERY>>,
        }>
    }
}
```

- В случае некорректного тела запроса ожидаем `400 Bad Request` со следующей схемой тела ответа:

```jsonc
{
    "status": "fail",
    "reasonCode": string,     # код ошибки (см. список возможных кодов ниже)
    "reason": string or null  # текстовое описание ошибки, например: "order error: ..."
}
```

| reasonCode         | Описание                                     |
|--------------------|----------------------------------------------|
| `OUT_OF_INVENTORY` | Товар более недоступен в заданном количестве |
| `ITEM_NOT_FOUND`   | Товар с указанным идентификатором не найден  |
| `OTHER`            | Иные причины                                 |

#### Получение детальной информации о точке самовывоза

`POST <base_url>/v1/pickup-option-details`

Тело запроса (payload JWT-токена):

```jsonc
{
    "merchantId": uuid,
    "currencyCode": string,
    "pickupPointId": string,
    "cart": {                   # Корзина c ценами, размером и весом товаров.
        "cartId": "string",
        "externalId": string,   # Опционально. Id корзины в системе продавца.
        "items": array<{
            "productId": string,
            "quantity": {
                "count": decimal ("42.00")
            }
        }>,
        "coupons": array<{
            "value": string
        }>
    },
    "metadata": string or null,
}
```

Ответ:

- В случае успеха ожидаем `200 OK` и детали точки самовывоза:

```jsonc
{
    "status": "success",
    "data": {
        "pickupOption": {
            "pickupPointId": string,            # Уникальный id точки самовывоза в системе продавца
            "title": string,                    # Название точки самовывоза
            "address": string,                  # Адрес в виде строки
            "provider": enum<PICKPOINT|...|IN_STORE>,
            "location": {
                "longitude": number,
                "latitude": number
            },

            "amount": decimal ("42.00"),        # Стоимость доставки в точку

            "fromDate": string,                 # YYYY-MM-DD. Ближайшая возможная дата доставки
            "toDate": string,                   # Опционально. YYYY-MM-DD. Самая поздняя дата доставки

            "description": string or null,      # Опционально. Дополнительное описание
            "phones": array<string> or null,    # Опционально. Телефоны для связи

            "schedule": [                       # Опционально. График работы точки.
                {
                    "label": string,            # Например, "пн-пт"
                    "fromTime": string,         # HH:MM, "08:00"
                    "toTime": string,           # HH:MM, "20:00"
                }
            ],

            "receipt": {...},                   # Опционально. Данные для формирования чека

            "storagePeriod": int,               # Опционально. Срок хранения товара в точке самовывоза в днях.

            # Опционально. Доступные методы оплаты заказа при выбранном способе самовывоза
            "allowedPaymentMethods": array<enum<CARD|SPLIT|CASH_ON_DELIVERY|CARD_ON_DELIVERY>>,
        }>
    }
}
```

- В случае некорректного запроса ожидаем `400 Bad Request` со следующей схемой тела ответа:

```jsonc
{
    "status": "fail",
    "reasonCode": string,     # код ошибки (см. список возможных кодов ниже)
    "reason": string or null  # текстовое описание ошибки, например: "order error: ..."
}
```

| reasonCode               | Описание                                                |
|--------------------------|---------------------------------------------------------|
| `OUT_OF_INVENTORY`       | Товар более недоступен в заданном количестве            |
| `ITEM_NOT_FOUND`         | Товар с указанным идентификатором не найден             |
| `PICKUP_POINT_NOT_FOUND` | Точка самовывоза с указанным идентификатором не найдена |
| `OTHER`                  | Иные причины                                            |

#### Коррекция опций Яндекс Доставки

`POST <base_url>/v1/yandex-delivery/adjust-options`

Тело запроса (payload JWT-токена):

```jsonc
{
    "merchantId": uuid,
    "cart": {                   # Корзина ценами, размером и весом товаров.
        "cartId": "string",
        "externalId": string,   # Опционально. Id корзины в системе продавца.
        "items": ...,
        ...
    },
    "yandexDeliveryOptions": [
        { ... }
    ]
}
```

Ответ:

- В случае успеха ожидаем `200 OK` и точки самовывоза:

```jsonc
{
    "status": "success",
    "data": {
        "yandexDeliveryOptions": [
            { ... }
        ]
    }
}
```

## Merchant -> Yandex Pay API

### Принцип работы

Передавайте следующие HTTP заголовки в ваших запросах:

- X-Request-Id: <уникальный идентификатор запроса>
- X-Request-Timeout: <таймаут запроса в миллисекундах>
- X-Request-Attempt: <номер попытки (0 — первая попытка, 1, 2 и т.д. — перезапросы)>

`X-Request-Id` нужен для отладки запросов, а также для обеспечения идемпотентности пишущих запросов.
Поэтому одно и то же значение `X-Request-Id` должно сохраняться во всех перезапросах
при получении ошибок с HTTP-кодами 5xx, либо 429 в ответ.

`X-Request-Timeout` для
[deadline propagation](https://sre.google/sre-book/addressing-cascading-failures/#deadline-propagation-1)
во время обработки запроса в системе.
Не используйте значения таймаутов меньше секунды. Рекомендуемые значения таймаутов — 10-20 секунд.

`X-Request-Attempt` полезен для общей диагностики.

### Аутентификация запроса продавца

Для использования API необходимо получить аутентификационный API-ключ.
Токен необходимо передавать для каждого запроса в HTTP-заголовке `Authorization`.
Управление ключами находится в [консоли Yandex Pay](https://console.pay.yandex.ru/web/account/developers).
При этом в sandbox окружении API-ключ равен значению `merchant_id`.

```text
--header 'Authorization: Api-Key <значение ключа>'
```

Если в запросе отсутствует токен или передан недействительный токен, сервер возвращает HTTP-статус `401 Unauthorized`.

### API вызовы со стороны бэкенда продавца в Yandex Pay

#### Получение деталей заказа

`GET /api/merchant/v1/orders/{orderId}`

- `orderId` - ID заказа на стороне продавца, который был передан в ответе на `/order/create`

Ответ:

- Детали заказа и список транзакций по возврату

```jsonc
{
    "status": "success",
    "data": {
        "order": {
            "orderId": string,

            "created": string,          # Дата и время создания заказа (ISO 8601)
            "updated": string,          # Дата и время обновления заказа (ISO 8601)

            "paymentStatus": enum<PENDING|AUTHORIZED|CAPTURED|VOIDED|REFUNDED|PARTIALLY_REFUNDED|FAILED>,
            "reason": string or null,   # причина (применимо для статусов VOIDED/FAILED)

            "orderAmount": decimal ("42.00"),   # текущая сумма заказа после прошедших списаний/возвратов
            "cart": {...},                      # текущая корзина
            "shippingMethod": {...},
            "paymentMethod": {...},
            "metadata": string or null
        },

        "delivery": {
            "price": decimal ("42.00"),                     # Цена доставки для покупателя
            "actualPrice": decimal ("42.00"),               # Опционально. Цена доставки для продавца
            "status": enum<ESTIMATING|COLLECTING|...>,      # Статус доставки
            "created": string,                              # Дата и время создания доставки (ISO 8601)
            "updated": string,                              # Дата и время обновления доставки (ISO 8601)
        },

        "operations": array<{
            "operationId": string,
            "operationType": enum<AUTHORIZE|REFUND|CAPTURE|VOID>,
            "amount": decimal ("42.00"),
            "status": SUCCESS,
        }>
    }
}
```

#### Получение деталей операции авторизации, списания, возврата или отмены платежа

`GET /api/merchant/v1/operations/{operationId or externalOperationId}`

Ответ:

```jsonc
{
    "status": "success",
    "data": {
        "operation": {
            "operationId": uuid,
            "externalOperationId": string,  # Идентификатор операции на стороне продавца

            "operationType": enum<AUTHORIZE|REFUND|CAPTURE|VOID>,

            "status": enum<PENDING|SUCCESS|FAIL>
            "reason": string or null,       # Причина FAIL

            "amount": decimal ("42.00"),    # Сумма операции

            "created": string,              # Дата и время создания операции (ISO 8601)
            "updated": string,              # Дата и время обновления операции (ISO 8601)
        }
    }
}
```

#### Отмена платежа

`POST /api/merchant/v1/orders/{orderId}/cancel`

Доступно только для платежей в статусе `AUTHORIZED`.
В случае успеха статус платежа изменится на `VOIDED`.

Тело запроса:

```jsonc
{
    "reason": string,                   # Причина отмены
    "externalOperationId": string       # Опционально. Идентификатор операции.
}
```

Ответ в случае успеха содержит детали операции отмены:

- 200 OK c телом:

    ```jsonc
    {
        "status": "success",
        "data": {
            "operation": {
                "operationId": uuid,
                "orderId": string,
                "operationType": "VOID",
                "status": "SUCCESS",
                "externalOperationId": string or null,
                "created": string,
                "updated": string
            }
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден
- 400 Bad Request - Некорректный запрос. Тело ответа:

    ```jsonc
    {
        "status": "fail",
        "reasonCode": enum<INVALID_PAYMENT_STATUS|BAD_REQUEST|...>,  # код ошибки
        "reason": string or null  # текстовое описание, например: "Captured payment cannot be cancelled"
    }
    ```

#### Подтверждение платежа

`POST /api/merchant/v1/orders/{orderId}/capture`

Списание заблокированных средств. Доступно только для платежей в статусе `AUTHORIZED`.
При успешном результате запроса статус платежа изменится на `CAPTURED`.

В случае передачи суммы подтверждения меньшей, чем оригинальная, оставшаяся часть платежа будет возвращена.
В данном случае нужно передать итоговую корзину предоставляемых товаров и услуг.
Итоговая корзина должна формироваться из текущей корзины исключением некоторых позиций, по которым производился возврат.

Тело запроса:

```jsonc
{
    "orderAmount": decimal ("84.00")    # Опционально. Сумма к списанию.
                                        # Если не указана, будет списана вся заблокированная сумма

    "cart": {                           # Опционально. Итоговая корзина
        "items": [...],
        "discounts": [...],
        "total": {
            "amount": decimal ("42.00")
        }
    },

    "shipping": {                       # Опционально. Итоговый способ доставки
        "methodType": enum<COURIER|PICKUP|YANDEX_DELIVERY>,
        "amount": decimal ("42.00"),
        "receipt": {...},
    },
    "externalOperationId": string,      # Опционально. Идентификатор операции.
}
```

Ответ в случае успеха содержит детали операции списания:

- 200 OK c телом:

    ```jsonc
    {
        "status": "success"
        "data": {
            "operation": {
                "operationId": uuid,
                "orderId": string,
                "operationType": CAPTURE,
                "status": enum<PENDING|SUCCESS>,
                "externalOperationId": string or null,
                "amount: decimal ("84.00"),
                "created": string,
                "updated": string
            }
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден
- 400 Bad Request - Некорректный запрос. Тело ответа:

    ```jsonc
    {
        "status": "fail",
        "reasonCode": enum<INVALID_PAYMENT_STATUS|ORDER_AMOUNT_MISMATCH|CAPTURE_AMOUNT_TOO_LARGE|...>,  # код ошибки
        "reason": string or null  # текстовое описание, например: "Cancelled payment cannot be captured"
    }
    ```

#### Возврат средств за заказ

`POST /api/merchant/v1/orders/{orderId}/refund`

Запуск возврата средств по заказу.
Доступно только для платежей в статусе `CAPTURED` и `PARTIALLY_REFUNDED`.
В случае успеха статус платежа изменится на `REFUNDED` или `PARTIALLY_REFUNDED` в зависимости от суммы
и будет отправлено событие `ORDER_STATUS_UPDATED`.
Если произвести возврат не удастся, то будет отправлено событие `OPERATION_STATUS_UPDATED`.

В запросе нужно передать итоговую корзину предоставляемых товаров и услуг.
Итоговая корзина должна формироваться из текущей корзины исключением некоторых позиций,
либо корректировкой стоимости имеющихся позиций, по которым производился возврат.
Сумма корзины должна совпадать с текущей суммой платежа за вычетом суммы возврата.

Тело запроса:

```jsonc
{
    "refundAmount": decimal ("42.00"),  # Сумма к возврату
    "orderAmount": decimal ("84.00"),   # Итоговая сумма заказа. Равна `cart.total.amount` + `shipping.amount`
    "cart": {                           # Итоговая корзина
        "items": [...],
        "discounts": [...],
        "total": {
            "amount": decimal ("42.00")
        }
    },
    "shipping": {
        "methodType": enum<COURIER|PICKUP|YANDEX_DELIVERY>,
        "amount": decimal ("42.00"),
        "receipt": {...},
    },
    "externalOperationId": string,      # Опционально. Идентификатор операции в системе продавца.
}
```

Ответ в случае успеха содержит детали операции возврата:

- 200 OK с телом:

    ```jsonc
    {
        "status": "success",
        "data": {
            "operation": {
                "operationId": uuid,
                "orderId": string,
                "operationType": REFUND,
                "status": enum<PENDING|SUCCESS>,
                "externalOperationId": string or null,
                "amount: decimal ("42.00"),
                "created": string,
                "updated": string
            }
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден
- 400 Bad Request - Некорректный запрос. Тело ответа:

    ```jsonc
    {
        "status": "fail",
        "reasonCode": enum<INVALID_PAYMENT_STATUS|ORDER_AMOUNT_MISMATCH|REFUND_AMOUNT_TOO_LARGE|...>,  # код ошибки
        "reason": string or null  # текстовое описание, например: "Refund amount should be less than order amount"
    }
    ```

### API вызовы для работы с доставкой

#### Инициирование доставки

`POST /api/merchant/v1/orders/{orderId}/delivery/create`

Запускается процесс расчета стоимости доставки.

Ответ в случае успеха:

- 200 OK c телом:

    ```
    {
        "status": "success",
        "data": {
            "delivery": {
                "price": decimal ("42.00"),        # Цена доставки для покупателя
                "status": enum<ESTIMATING|...>,    # Текущий статус доставки
                "created": string,                 # Дата и время создания доставки (ISO 8601)
                "updated": string,                 # Дата и время обновления доставки (ISO 8601)
            }
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден

#### Подтверждение доставки

`POST /api/merchant/v1/orders/{orderId}/delivery/accept`

Доступно только в статусе `READY_FOR_APPROVAL`.

Ответ в случае успеха:

- 200 OK c телом:

    ```
    {
        "status": "success",
        "data": {
            "delivery": {
                "price": decimal ("42.00"),            # Цена доставки для покупателя
                "actualPrice": decimal ("42.00"),      # Опционально. Цена доставки для продавца
                "status": enum<COLLECTING|...>,        # Текущий статус доставки
                "created": string,
                "updated": string,
            }
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден
- 400 Bad Request - Некорректный запрос. Тело ответа:

    ```jsonc
    {
        "status": "fail",
        "reasonCode": enum<INVALID_DELIVERY_STATUS|...>,  # код ошибки
        "reason": string or null  # текстовое описание
    }
    ```

#### Обновление доставки

`POST /api/merchant/v1/orders/{orderId}/delivery/renew`

Доступно только в статусе `EXPIRED`.

Ответ в случае успеха содержит информацию о доставке:

- 200 OK c телом:

    ```
    {
        "status": "success",
        "data": {
            "delivery": {...}
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден
- 400 Bad Request - Некорректный запрос. Тело ответа:

    ```jsonc
    {
        "status": "fail",
        "reasonCode": enum<INVALID_DELIVERY_STATUS|...>,  # код ошибки
        "reason": string or null  # текстовое описание
    }
    ```

#### Получение информации о возможности отмены

`POST /api/merchant/v1/orders/{orderId}/delivery/cancel-info`

Ответ в случае успеха:

- 200 OK c телом:

    ```
    {
        "status": "success",
        "data": {
            "cancelState": enum<FREE|PAID|UNAVAILABLE>
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден

#### Отмена доставки

`POST /api/merchant/v1/orders/{orderId}/delivery/cancel`

Запуск операции по отмене доставки.

Бесплатная отмена доступна для статусов `ESTIMATING`, `EXPIRED`, `READY_FOR_APPROVAL`, `COLLECTING`.
Платная отмена доступна для статуса `PREPARING` и в некоторых случаях для статуса `DELIVERING`.

Тело запроса:

```jsonc
{
    "cancelState": enum<FREE|PAID>  # Статус отмены (платная или бесплатная)
}
```

Ответ в случае успеха:

- 200 OK c телом:

    ```
    {
        "status": "success",
        "data": {
            "delivery": {
                ...
            }
        }
    }
    ```

Ответ в случае ошибки:

- 404 Not Found - Заказ с указанным `orderId` не найден
- 400 Bad Request - Некорректный запрос. Тело ответа:

    ```jsonc
    {
        "status": "fail",
        "reasonCode": enum<STATE_MISMATCH|INVALID_DELIVERY_STATUS...>,  # код ошибки
        "reason": string or null  # текстовое описание
    }
    ```

## Отправка чеков в ФНС (54-ФЗ)

Для автоматического формирования чеков, нужно в ответе `order/render`
для товаров в корзине (`cart.items`) и вариантов доставки (`shipping.availableCourierOptions`),
и в ответе `pickup-option-details` для опций самовывоза заполнить объект `receipt` следующего формата:

```jsonc
{
    "title": string,                    # Опционально. 1030: Наименование предмета расчета
                                        # Если не указан, будет заполнен значением title родительского объекта
    "tax": int,                         # 1199: Ставка НДС (значения в Таблице 1)
    "measure": int,                     # 2108: Код единиц измерения (значения в Таблице 2)
    "paymentMethodType": int            # Опционально. 1214: Способ расчета (значения в Таблице 3)
    "paymentSubjectType": int           # Опционально. 1212: Предмет расчета (значения в Таблице 4)
    "excise": decimal("100.0")          # Опционально. 1229: Акциз
    "productCode": string               # Опционально. 1162: Код товара (base64 кодированный массив от 1 до 32 байт)
    "markQuantity": {                   # Опционально. 1291: Дробное количество маркированного товара
        "numerator": int,               # 1293: Числитель
        "denominator": int,             # 1294: Знаменатель
    },
    "supplier": {                       # Опционально. 1224: Данные поставщика
        "name": string,                 # 1225: Наименование поставщика
        "inn": string,                  # 1226: ИНН поставщика
        "phones": array<string>,        # 1171: Телефоны поставщика в формате +79995554444
    },
    "agent": {                          # Опционально. 1223: Данные агента
        "agentType": int,               # 1222: Признак агента по предмету расчета (значения в Таблице 5)
        "operation": string             # 1044: Операция платежного агента
        "phones": array<string>,        # 1073: Телефоны платежного агента в формате +79995554444
        "transferOperator": {
            "name": string,             # 1026: Наименование оператора перевода
            "address": string,          # 1005: Адрес оператора перевода
            "inn": string,              # 1016: ИНН оператора перевода
            "phones: array<string>,     # 1075: Телефоны оператора перевода в формате +79995554444
        },
        "paymentsOperator": {
            "phones: array<string>,     # 1074: Телефоны оператора по приему платежей в формате +79995554444
        }
    }
}
```

### Таблица 1. Значения `tax` - «ставка НДС» (тег 1199)

| Значение | Описание                       |
|----------|--------------------------------|
| 1        | НДС по ставке 20%              |
| 2        | НДС по ставке 10%              |
| 3        | НДС по расчетной ставке 20/120 |
| 4        | НДС по расчетной ставке 10/110 |
| 5        | НДС по ставке 0%               |
| 6        | Без НДС                        |

#### Таблица 2. Значения `quantity.measure` - «мера количества предмета расчета» (тег 2108)

| Значение | Описание                                         |
|----------|--------------------------------------------------|
| 0        | Штуки или единицы                                |
| 10       | Грамм                                            |
| 11       | Килограмм                                        |
| 12       | Тонна                                            |
| 20       | Сантиметр                                        |
| 21       | Дециметр                                         |
| 22       | Метр                                             |
| 30       | Квадратный сантиметр                             |
| 31       | Квадратный дециметр                              |
| 32       | Квадратный метр                                  |
| 40       | Миллилитр                                        |
| 41       | Литр                                             |
| 42       | Кубический метр                                  |
| 50       | Киловатт час                                     |
| 51       | Гигакалория                                      |
| 70       | Сутки (день)                                     |
| 71       | Час                                              |
| 72       | Минута                                           |
| 73       | Секунда                                          |
| 80       | Килобайт                                         |
| 81       | Мегабайт                                         |
| 82       | Гигабайт                                         |
| 83       | Терабайт                                         |
| 255      | Применяется при использовании иных мер измерения |

#### Таблица 3. Значения `paymentMethodType` - «признак способа расчета» (тег 1214)

| Значение | Описание                                                                                      |
|----------|-----------------------------------------------------------------------------------------------|
| 1        | полная предварительная оплата до момента передачи предмета расчета                            |
| 2        | частичная предварительная оплата до момента передачи предмета расчета                         |
| 3        | аванс                                                                                         |
| 4        | полная оплата в момент передачи предмета расчёта                                              |
| 5        | частичная оплата предмета расчёта в момент его передачи с последующей оплатой в кредит        |
| 6        | передача предмета расчёта без его оплаты в момент его передачи с последующей оплатой в кредит |
| 7        | оплата предмета расчёта после его передачи с оплатой в кредит                                 |

#### Таблица 4. Значения `paymentSubjectType` - «признак предмета расчета» (тег 1212)

| Значение | Описание                                                                                                                       |
|----------|--------------------------------------------------------------------------------------------------------------------------------|
| 1        | товар                                                                                                                          |
| 2        | подакцизный товар                                                                                                              |
| 3        | работа                                                                                                                         |
| 4        | услуга                                                                                                                         |
| 5        | ставка азартной игры                                                                                                           |
| 6        | выигрыш азартной игры                                                                                                          |
| 7        | лотерейный билет                                                                                                               |
| 8        | выигрыш лотереи                                                                                                                |
| 9        | предоставление РИД                                                                                                             |
| 10       | платёж                                                                                                                         |
| 11       | агентское вознаграждение                                                                                                       |
| 12       | составной предмет расчёта                                                                                                      |
| 13       | иной предмет расчёта                                                                                                           |
| 14       | имущественное право                                                                                                            |
| 15       | внереализационныи доход                                                                                                        |
| 16       | страховые взносы: о суммах расходов, уменьшающих сумму налога (авансовых платежей) в соответствии с п. 3.1 статьи 346.21 НК РФ |
| 17       | торговыи сбор                                                                                                                  |
| 18       | курортныи сбор                                                                                                                 |
| 19       | залог                                                                                                                          |
| 20       | расход: о суммах произведенных расходов в соответствии со статьей 346.16 НК РФ, уменьшающих доход                              |
| 21       | взносы на обязательное пенсионное страхование ИП                                                                               |
| 22       | взносы на обязательное пенсионное страхование                                                                                  |
| 23       | взносы на обязательное медицинское страхование ИП                                                                              |
| 24       | взносы на обязательное медицинское страхование                                                                                 |
| 25       | взносы на обязательное социальное страхование                                                                                  |
| 26       | платеж казино                                                                                                                  |

#### Таблица 5. Значения `agent.agentType` «признак агента по предмету расчета» (тег 1222)

| Значение | Описание                      |
|----------|-------------------------------|
| 1        | банковский платёжный агент    |
| 2        | банковский платёжный субагент |
| 3        | платёжный агент               |
| 4        | платёжный субагент            |
| 5        | поверенный                    |
| 6        | комиссионер                   |
| 7        | иной агент                    |
