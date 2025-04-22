## Примеры запросов

### Запрос платежных методов
```
curl --location --request GET 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/method/gate/trust' \
--header 'X-Vertis-User: 1'
```
```
[
  {
    "editable": false,
    "method": "card",
    "name": "Новая карта",
    "properties": {
      "currency": "RUB",
      "firmId": 12,
      "paymentSystems": [
        "MIR",
        "Maestro",
        "MasterCard",
        "VISA",
        "VISA_ELECTRON"
      ]
    },
    "system": "trust"
  }
]
```
### Пополнение кошелька (через WEB форму)
```
curl --location --request POST 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/payment/trust/method/card' \
--header 'X-Vertis-User: 1' \
--header 'X-Forwarded-For: 127.0.0.1' \
--header 'X-Yandex-Uid: 1122334455' \
--header 'Content-Type: application/json' \
--data-raw '{
    "account": "user:69972641",
    "amount": 1050,
    "context": {
        "target": "Wallet"
    },
    "options": {
        "defaultURL": "https://test.avto.ru/my/wallet/"
    },
    "payGateContext": {
        "trustContext": {
            "payment_data": {
                "type": "WEB_PAYMENT"
            },
            "orders": [
              {
                "product_id": "wallet",
                "quantity": 1,
                "price": 1050
              }
            ]
        }
    },
    "receipt": {
        "email": "den-korobov@yandex-team.ru",
        "phone": "+791112223344",
        "goods": [
            {
                "name": "Пополнение кошелька",
                "quantity": 1,
                "price": 1050
            }
        ]
    },
    "payload": {}
}'
```
```
{
    "confirmationType": "redirect",
    "id": "1c4bd575-24f5-4de0-93e1-5290ee331ce7",
    "purchaseToken": "14f6e9c672103aae4571d112b17805db",
    "url": "https://trust-test.yandex.ru/web/payment?purchase_token=14f6e9c672103aae4571d112b17805db"
}
```
### Оплата услуги (через WEB форму)
```
curl --location --request POST 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/payment/trust/method/card' \
--header 'X-Vertis-User: 1' \
--header 'X-Forwarded-For: 127.0.0.1' \
--header 'X-Yandex-Uid: 1122334455' \
--header 'Content-Type: application/json' \
--data-raw '{
    "account": "user:69972641",
    "amount": 9900,
    "context": {
        "target": "Purchase"
    },
    "options": {
        "defaultURL": "https://test.avto.ru/my/"
    },
    "payGateContext": {
        "trustContext": {
            "payment_data": {
                "type": "WEB_PAYMENT"
            },
            "orders": [
              {
                "product_id": "boost",
                "quantity": 1,
                "price": 9900
              }
            ]
        }
    },
    "receipt": {
        "email": "den-korobov@yandex-team.ru",
        "phone": "+791112223344",
        "goods": [
            {
                "name": "Поднятие в поиске",
                "quantity": 1,
                "price": 9900
            }
        ]
    },
    "payload": {
        "json": {
          "domain": "autoru",
          "transaction": "{salesman_transaction_id}"
        }
    }
}'
```
```
{
    "confirmationType": "redirect",
    "id": "03853758-460f-43ea-801f-5f5bead887d3",
    "purchaseToken": "970ca18d331d4dcd955082109b44079e",
    "url": "https://trust-test.yandex.ru/web/payment?purchase_token=970ca18d331d4dcd955082109b44079e"
}
```
### Оплата услуги с кошелька
```
curl --location --request PUT 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/account/user:69972641/consume' \
--header 'X-Vertis-User: 1' \
--header 'X-Forwarded-For: 127.0.0.1' \
--header 'X-Yandex-Uid: 1122334455' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "f7526f82-5ae7-4033-af7b-c2e3d6aa1324",
    "account": "user:69972641",
    "amount": 9900,
    "context": {
        "target": "Purchase"
    },
    "options": {
        "defaultURL": "https://test.avto.ru/my/"
    },
    "receipt": {
        "email": "den-korobov@yandex-team.ru",
        "phone": "+791112223344",
        "goods": [
            {
                "name": "Поднятие в поиске",
                "quantity": 1,
                "price": 9900
            }
        ]
    },
    "payload": {
        "json": {
          "domain": "autoru",
          "transaction": "{salesman_transaction_id}"
        }
    }
}'
```
```
{
    "account": "user:69972641",
    "activity": "Active",
    "id": {
        "id": "f7526f82-5ae7-4033-af7b-c2e3d6aa1324",
        "type": "Withdraw"
    },
    "income": 0,
    "overdraft": 0,
    "payload": {
        "json": {
            "domain": "autoru",
            "transaction": "{salesman_transaction_id}"
        }
    },
    "receipt": {
        "email": "den-korobov@yandex-team.ru",
        "goods": [
            {
                "name": "Поднятие в поиске",
                "price": 9900,
                "quantity": 1
            }
        ],
        "phone": "+791112223344"
    },
    "refund": 0,
    "target": "Purchase",
    "timestamp": "2022-04-01T14:17:22.240+03:00",
    "user": "user:69972641",
    "withdraw": 9900
}
```
### Рекуррентная оплата услуги с привязанной карты
```
curl --location --request POST 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/payment/trust/method/card-x75ab11a2dbdd17dba2e35443' \
--header 'X-Vertis-User: 1' \
--header 'X-Forwarded-For: 127.0.0.1' \
--header 'X-Yandex-Uid: 1122334455' \
--header 'Content-Type: application/json' \
--data-raw '{
    "account": "user:69972641",
    "amount": 9900,
    "context": {
        "target": "Purchase"
    },
    "options": {
        "defaultURL": "https://test.avto.ru/my/"
    },
    "payGateContext": {
        "trustContext": {
            "payment_data": {
                "type": "API_PAYMENT"
            },
            "orders": [
              {
                "product_id": "boost",
                "quantity": 1,
                "price": 9900
              }
            ]
        }
    },
    "receipt": {
        "email": "den-korobov@yandex-team.ru",
        "phone": "+791112223344",
        "goods": [
            {
                "name": "Поднятие в поиске",
                "quantity": 1,
                "price": 9900
            }
        ]
    },
    "payload": {
        "json": {
          "domain": "autoru",
          "transaction": "{salesman_transaction_id}"
        }
    }
}'
```
```
{
    "confirmationType": "redirect",
    "id": "4f91b96b-461c-4f65-82ea-f6a1fec10bcb",
    "purchaseToken": "80f216a093a98d79a62c938f6da7af11"
}
```
### Рекуррентная оплата с кошелька либо с любой привязанной карты (aka "сделай красиво")
```
curl --location --request POST 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/payment/trust/recurrent' \
--header 'X-Vertis-User: 1' \
--header 'X-Forwarded-For: 127.0.0.1' \
--header 'X-Yandex-Uid: 1122334455' \
--header 'Content-Type: application/json' \
--data-raw '{
    "externalId": "{salesman_transaction_id}",
    "account": "user:69972641",
    "amount": 9900,
    "context": {
        "target": "Purchase"
    },
    "payGateContext": {
        "trustContext": {
            "payment_data": {
                "type": "API_PAYMENT"
            },
            "orders": [
              {
                "product_id": "boost",
                "quantity": 1,
                "price": 9900
              }
            ]
        }
    },
    "receipt": {
        "email": "den-korobov@yandex-team.ru",
        "phone": "+791112223344",
        "goods": [
            {
                "name": "Поднятие в поиске",
                "quantity": 1,
                "price": 9900
            }
        ]
    },
    "payload": {
        "json": {
          "domain": "autoru",
          "transaction": "{salesman_transaction_id}"
        }
    },
    "strategy": "WalletAndAttachedCards"
}'
```
```
200 OK
{
    "status": "IN_PROGRESS"
}
```
### Частичный возврат (только для кошелька)
```
curl --location --request POST 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/payment/trust/67daf38a-fbfd-4104-9337-05614c4d5832/refund?amount=50' \
--header 'X-Vertis-User: 1' \
--header 'Content-Type: application/json' \
--data-raw '{
  "comment": "Refund from localhost",
  "receipt": {
    "goods": [
      {
        "name": "Пополнение кошелька",
        "quantity": 1,
        "price": 50
      }
    ],
    "email": "den-korobov@yandex-team.ru",
    "phone": "+791112223344"
  }
}'
```
```
{
    "message": "OK"
}
```
### Полный возврат
```
curl --location --request DELETE 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/payment/trust/a8a3565a-257b-4b68-9fba-ee84ecfc1540?comment=Full refund from localhost
' \
--header 'X-Vertis-User: 1' \
--header 'X-Forwarded-For: 127.0.0.1'
```
```
{
    "message": "OK"
}
```
### Оплата услуг картой со списанием баллов Плюса
```
curl --location --request POST 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/payment/trust/method/card' \
--header 'X-Vertis-User: 1' \
--header 'X-Forwarded-For: 127.0.0.1' \
--header 'X-Yandex-Uid: 1122334455' \
--header 'Content-Type: application/json' \
--data-raw '{
    "account": "user:69972641",
    "amount": 9900,
    "context": {
        "target": "Purchase"
    },
    "options": {
        "defaultURL": "https://test.avto.ru/my/"
    },
    "payGateContext": {
        "trustContext": {
            "payment_data": {
                "type": "WEB_PAYMENT"
            },
            "orders": [
              {
                "product_id": "boost",
                "quantity": 1,
                "price": 9900
              }
            ],
            "plusWithdraw": {
                "amount": "9800"
            }
        }
    },
    "receipt": {
        "email": "den-korobov@yandex-team.ru",
        "phone": "+791112223344",
        "goods": [
            {
                "name": "Поднятие в поиске",
                "quantity": 1,
                "price": 9900
            }
        ]
    },
    "payload": {
        "json": {
          "domain": "autoru",
          "transaction": "{salesman_transaction_id}"
        }
    }
}'
```
```
{
    "confirmationType": "redirect",
    "id": "03853758-460f-43ea-801f-5f5bead887d3",
    "purchaseToken": "970ca18d331d4dcd955082109b44079e",
    "url": "https://trust-test.yandex.ru/web/payment?purchase_token=970ca18d331d4dcd955082109b44079e"
}
```
### Обновление разметки корзины
```
curl --location --request PUT 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user%3A69972641/payment/trust/d9c7b19e-c6de-41f1-acfb-a35f402eb7d1/markup' \
--header 'X-Vertis-User: 1' \
--header 'Content-Type: application/json' \
--data-raw '{
    "withdraw": 100
}'
```
```
{
    "message": "OK"
}
```
### Получение баланса бонусного аккаунта
```
curl --location --request GET 'http://banker-api-http-api.vrts-slb.test.vertis.yandex.net/api/1.x/service/autoru/customer/user:69972641/method/gate/trust/method/yandex_account' \
--header 'X-Vertis-User: 1' \
--header 'X-Yandex-Uid: 1122334455'
```
```
[
    {
        "editable": false,
        "method": "yandex_account-w/6bafa736-9c1e-5d06-8c6f-59b9f4d1f316",
        "properties": {
            "balance": 7500,
            "currency": "RUB"
        },
        "system": "trust"
    }
]
```
