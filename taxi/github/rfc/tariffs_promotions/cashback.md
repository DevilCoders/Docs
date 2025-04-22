## Промотирование повышенных тарифов с доплатой плюсом

### Продуктовое описание
См. описание тикета [TAXIPROJECTS-2021](https://st.yandex-team.ru/TAXIPROJECTS-2021)
![Дизайн](img/cashback.png)

## Верхнеуровневое описание механики

Работаем через альтернативный оффер, который содержит частичную оплату плюсом.
Изначально оффер не отображается в приложении.

При включении переключателя на промо:
- альт. оффер заменяет базовый оффер для конкретного тарифа
- редиректим на альт. оффер.

При выключении переключателя на промо - скрываем альт. оффер и показываем базовый.

Если пользователь делает заказ с альт. оффером, то в orderdraft в способ оплаты необходимо добавить,
что пользователь выбрал частичную оплату плюсом и количество баллов из альт. оффера.

*Замечание: если пользователь увидел промо с оплатой баллами,
но в этот момент потратил их в другом месте, то сработает стандратная логика кэшбека:
заказ можно будет создать, стоимость поездки полностью спишется с основного способа оплаты.*

---

## Backend-реализация

### routestats

Альтернативный оффер создается, если:
1) применима логика обычного плюса
2) заказ с точкой Б
3) запрос без оплаты баллами плюса 
4) пользователь попадает в эксперимент промо
5) для пользователя выполняются условия промо
6) у пользователя достаточно баллов плюса для промо

В pdp дополнительно рассчитываем количетство баллов и новую цену с учетом баллов.
После этого формируем альтернативный оффер, аналогичный офферу, когда включена оплата плюсом.


Чтобы старым клиентам не возвращался новый тип альт.оффера, клиенты явно будут говорить, что его поддерживают.

Сейчас в запросе routestats уже есть поля:

```
{
    ...
    "supports_no_cars_available": true,
    "supports_forced_surge": true,
    "supports_hideable_tariffs": true,
    "supports_paid_options": true,
    "supports_explicit_antisurge": true,
    "supports_multiclass": true,
    ...
}
```

Предлагается новые поля класть в структуру supports, чтобы:
1. сгруппировать значения
2. убрать повторения supports

```
{
    ...
    "supports": {
        "no_cars_available": true,
        "forced_surge": true,
        "hideable_tariffs": true,
        "paid_options": true,
        "explicit_antisurge": true,
        "multiclass": true,
        "plus_promo_alternative": true  // Для нашего оффера
    }

    ...
}
```

На бекенде поддерживать 2 варианта, в будущем, если предоставится возможность - удалить поддержку первого варианта.



Ответ routestats:
```json
{
  "alternatives": {
    ...,
    "options": [
      {
        ...,
        "offer": "...",
        "type": "plus_promo",
        "personal_wallet_withdraw_amount": "60"
      }
    ]
  },
  ...
}
```

### pdp
Сейчас есть правило только полного списания с кошелька [personal_wallet_complement](https://tariff-editor.taxi.yandex-team.ru/price-conversion-rules/view/319).

Для альт. оффера расчитываем дополнительную цену с учетом настроек промо.

### uroutestats
Cохраняем из альт. оффера кол-во баллов плюса в tariffs-promotions

### tariffs-promotions
Через inapp-communication передаем альт. оффер id.

Из редиса достаем количество баллов и формируем toggle-промоплашку, в которой для каждого положения переключатель описываем какой выводить текст и что должно происходить в интерфейсе.

В этой плашке будет передаваться альт. оффер id, чтобы клиенты понимали какой оффер нужно показывать.

Запрос в inapp-communication:
```json
{
  ...
  "summary_state": {
    ...,
    "alternative_offers": [
      {
        ...,
        "offer_id": "...",
        "type": "plus_promo"
      }
    ]
  }
}
```

Ответ inapp-communication:
```json
{
  ...,
  "offers": {
    "promoblocks": {
      ...,
      "items": [
        {
          "id": "id_cashback_promo",
          "meta_type": "tariff_upgrade_cashback_promo",
          "supported_classes": [
            "econom"
          ],
          "text": {
            "items": [
              {
                "text": "Потратить баллы плюса",
                "type": "text"
              }
            ]
          },
          "title": {
            "items": [
              {
                "text": "Уехать на комфорте за",
                "type": "text"
              },
              {
                "text": "50 баллов",
                "type": "text",
                "meta_color": "plus"
              }
            ]
          },
          "widgets": {
            "toggle": {
              "is_selected": false,
              "on": {
                "actions": [
                  {
                    "type": "offer_substitution",
                    "offer": "alternative_offer_id",
                    "tariff": "comfort"
                  },
                  {
                    "type": "tariff_redirect",
                    "tariff": "comfort"
                  }
                ]
              },
              "off": {
                "actions": [
                  {
                    "type": "offer_substitution",
                    "offer": "main_offer_id",
                    "tariff": "comfort"
                  }
                ]
              }
            }
          }
        }
      ]
    }
  }
}
```

### orderdraft

```json
orderdraft request для обычного оффера:

"payment": {
  "complements": [],
  "payment_method_id": "card-xf947f682c16af2f926120429",
  "type": "card"
}


orderdraft request для альт.оффера plus_promo:

"payment": {
  "complements": [
    {
      "payment_method_id": "w/e65f188b-1089-5211-8dfe-aa1b1f836a2c",
      "type": "personal_wallet",
      "withdraw_amount": "60"
    }
  ],
  "payment_method_id": "card-xf947f682c16af2f926120429",
  "type": "card"
}
```

---

## Какие варианты еще были рассмотрены?

1. Передавать информацию о доплате плюсом в отдельном полем в service_levels.

Не подходит, т.к. баллы плюса нужно прогонять через pdp, чтобы он сформировал новый оффер, который где-то нужно еще хранить.

2. Передавать баллы в orderdraft

Аналогичному первому решению, нужно делать перерасчет оффера. При этом, в orderdraft передаются параметры либо для подтверждения фиксы, либо для заказа по таксометру.
