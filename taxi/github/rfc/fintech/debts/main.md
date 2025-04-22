# Долги по яндекс карте

## Дизайн первой итерации
![This is an image](imgs/design.png)

## Общие сведения

Пользователь может в долг по различным причинам: технические, недостаток средств или любой другой. 
Что хочется: 
* Дать возможность пользователю оплатить долг яндекс картой (уже есть)
* Подсказать на какую сумму можно пополнить (первый фрейм на скрине выше)
* Если оплата не прошла, то сказать почему


## Как это будет работать

Вся информация по долгам и о текущем состоянии заказа (оплачивается или оплата прошла неуспешно) приходит в ручке paymentstatuses

Пример ответа (то что приходит сейчас)
```
{
  "cards": [
  ],
  "orders": [
    {
      "can_be_paid_by": [
        {
          "type": "applepay"
        },
        {
          "type": "card"
        },
        {
          "type": "googlepay"
        },
        {
          "type": "yandex_card"
        }
      ],
      "can_be_paid_by_card": true,
      "created": "2022-03-01T15:21:21+0000",
      "currency_rules": {
        "code": "RUB",
        "sign": "₽",
        "template": "$VALUE$ $SIGN$$CURRENCY$",
        "text": "руб."
      },
      "orderid": "0fbb7f2e0fd53cbdbb998dda90deb226",
      "payment": {
        "cardid": "yabank_wallet-wa_1FAuFMU9R7y0pCAVAJRyNQ",
        "debt_detail": [
          {
            "cost": 3029,
            "cost_as_str": "3029 $SIGN$$CURRENCY$",
            "type": "ride"
          }
        ],
        "need_accept": false,
        "need_cvn": false,
        "status": "processing",
        "trust_payment_id": "621e3a78910d39352b85a429"
      },
      "services": [
        {
          "cost": 3029,
          "cost_as_str": "3029 $SIGN$$CURRENCY$",
          "type": "ride"
        },
        {
          "cost": 0,
          "cost_as_str": "0 $SIGN$$CURRENCY$",
          "type": "tips"
        }
      ],
      "tips": {
        "type": "percent",
        "value": 0
      }
    }
  ],
  "overdraft_available": true
}
```

Для конкретной информации о том что пользователь в данном случае может сделать появится новая структура order_status_window

Важно: бекенд не может знать баланс яндекс карты, поэтому сумму для пополнения необходимо считать на стороне клиентов, для этого необходимо отдельно передавать сумму долга пользователя, оно будет лежать в поле debt_sum

Пример ответа с новой структурой:

```
{
  "cards": [...],
  "orders": [...],
  "overdraft_available": true,
  "debt_flow": {
    "notification": {
      "order_status_window": {
        "alternative_payment_methods_text": "Выбрать другой способ оплаты", // текст кнопки выбора другого способа оплаты
        "currency_rules": {
          "code": "RUB",
          "sign": "₽",
          "template": "$VALUE$ $SIGN$$CURRENCY$",
          "text": "руб."
        },
        "debt_sum": 3821, // сумма всех запрошенных долгов по яндекс карте
        "icon_tag": "yandex_card_debt_notification", // иконка из левого верхнего угла нотификации
        "main_button": { // кнопка внизу нотификации
          "action": {
            "type": "bank_sdk_topup"
          },
          "text": "Пополнить"
        },
        "payment_method_id": "card-xa1e832a19bc83d34bcfcd47c", // способ оплаты
        "payment_type": "yandex_card", // типо платы
        // основной текст нотификации
        "text": "У вас долг $VALUE$ $SIGN$$CURRENCY$. Погасите его со счёта в Яндексе и получите кешбэк баллами Плюса.",
        "title": "Пополните счёт, чтобы оплатить долг $VALUE$ $SIGN$$CURRENCY$" // заголовок
      }
    }
  },
}
```
