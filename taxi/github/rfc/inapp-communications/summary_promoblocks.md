## Бизнесовая задача

Данный блок rfc развивает мысль описанную здесь: https://github.yandex-team.ru/taxi/rfc/pull/435/files
Продуктовое описание тут: https://st.yandex-team.ru/TAXIBACKEND-29436

## Предложение архитектуры в рамках rfc

![promo_products](https://jing.yandex-team.ru/files/ihelos/promo_products.png "promo_products")

Краткие детали реализации:
- Новый endpoint 
```
POST /4.0/inapp-communications/promos-on-summary
```
p.s. назвал по аналогии с существующей ручкой /4.0/inapp-communications/promos-on-map
имхо, лучше /4.0/inapp-communications/summary/promotions, но еще лучше единообразие
- В рамках этого endpoint'а осуществляется поход в источники промоблоков
- Также осуществляется поход во внешний источник, который определяет приоритет выдачи промоблоков

#### Коды ответов:
- `200` - ok
- `500` - ретраить не чаще чем указано в заголовке Retry-After (в секундах)
Если заголовка нет - не ретраим вовсе.

### Продуктовые ограничения

#### Этап 1

Реализация MVP

Что умеем:
- подключение новых источников саммари;
- приоритезированная отдача кастомизируемых промоблоков;

Ограничения первой реализации:
- невозможно использовать цены из routestats;
- каждый источник сам занимается генерацией и кастомизацией промоблока;

**Запрос:**
```json5
{
    "summary_state": {
        "offer_id": "some_offer_id", // идентификатор, которые позволит в будущем выгрузить цены
        "tariff_classes": ["econom", "vip"] // список тарифов доступных пользователю (из ответа routestats), required: true
    },
    "payment": {
        "type": "card",
        "payment_method_id": "card-x208169c9d6367b1b278c8d97",
        "complements": [ // required: false
            {
                "type": "card",
                "payment_method_id": "card-x208169c9d6367b1b278c8d97"
            }
        ]
    },
    "state": {
       "location": [lon, lat]
       "accuracy": ...,
       "bbox": [ 37.615, 55.758, 37.619, 55.753 ],
       "known_orders": [  по аналогии с v1/products
           "taxi:<taxi_order_id>:revision", 
           "eats:<eats_order_id>", 
           "grocery:<grocery_order_id>"
       ],
       fields: [{
           "type": "a",
           "position": [lon, lat],
           "uri": "ymapsbm1:\/\/org?oid=1351660327",
           "entrance": "6"
       } /* "b", "mid1", "mid2", etc */],
       l10n: {
           // as in `/suggest` endpoint
       },
       "nz": "moscow"
   },
  "client_info": {
      "supported_features": [
        {"type": "promoblock", "widgets": ["deeplink_arrow_button", "attributed_text"]}
      ],
      "mdash_width": 20.0, // добавил, так как потенциально можем заниматься "вмещением" текста в промоблок
      "ndash_width": 9.0,
  },
 "media_size_info": { // формально был бы не против воткнуть в client_info, но кажется для единообразия с другими ручками стоит оставить здес
    "screen_height": 1920,
    "screen_width": 1080,
    "scale": 2.5
  },
}
```

**Ответ:**
```json5
{
  "layout": { // по аналогии с v1/products
    "grid_id": "some_id", // идентификатор выдачи (блендера), необходим для аналитики
    "type": "promoblock_list", // вводим новый тип выдачи
  },
  "offers": { // опять же, по аналогии с v1/products и offers и items
    // потенциально здесь могут отдаваться другие типы промоблоков саммари, например нотификации, как это сейчас сделано с нотификацией о более низкой цене 
    "promoblocks": { // офферы промоблоков
      "items":  [
         {
          "id": "5cc0e8eb0c69ff1a8a364b37",
          "title": {
             "items": [
                    {
                        "type": "image",
                        "image_tag": "ets_badge_icon",
                        "width": 15,
                        "vertical_alignment": "center",
                        "color": "#000000",
                    },
                    {
                        "type": "text",
                        "text": "Еда: доставка за N минут",
                        "font_size": 14,
                        "font_weight": "bold",
                        "font_style": "italic",
                        "color": "#000000"
                    }
                ]
          },
          "text": {
             "items": [
                    {
                        "type": "image",
                        "image_tag": "ets_badge_icon",
                        "width": 15,
                        "vertical_alignment": "center",
                        "color": "#000000",
                    },
                    {
                        "type": "text",
                        "text": "Еда: доставка за N минут",
                        "font_size": 14,
                        "font_weight": "bold",
                        "font_style": "italic",
                        "color": "#000000"
                    }
                ]
          },
          "icon": { // раньше был "icon": "url"
            "image_tag": "...",
            "image_url": "..."
            // при наличии и image_tag и image_url
            // image_url приоритетнее,
            // + оставил icon, а не оставил в rich text'е, так как под нее по дизайну отдельный блок, не сдвигающий текст
          },
          "cashback": {
            "amount": "10"
            // Отображается картинка с кэшбэком - всегда справа от title
            // для многострочного title - горизонтальное выравнивание по first baseline
            // параметры отображения определяются клиентом
          },
          "widgets": {
              "deeplink_arrow_button": { // https://jing.yandex-team.ru/files/ihelos/2020-07-08%2009.13.40.jpg
              // даже если визуальный стиль виджета совпадает, если захочется поменять action - надо создать новый тип 
              // предлагаю так делать, тк есть подозрение, что `виджет` M<->M `action` усложнит разработку, и не сделает жизнь сильно легче 
                "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
                "color": "afafaf", // цвет стрелки
                "items": [
                    {
                        "type": "image",
                        "image_tag": "ets_badge_icon",
                        "width": 15,
                        "vertical_alignment": "center",
                        "color": "#000000",
                    },
                    {
                        "type": "text",
                        "text": "Еда: доставка за N минут",
                        "font_size": 14,
                        "font_weight": "bold",
                        "font_style": "italic",
                        "color": "#000000"
                    }
                ]
              },
              "attributed_text": { // https://jing.yandex-team.ru/files/ihelos/2020-07-08%2009.13.14.jpg
                  "items": [
                    {
                        "type": "image",
                        "image_tag": "ets_badge_icon",
                        "width": 15,
                        "vertical_alignment": "center",
                        "color": "#000000",
                    },
                    {
                        "type": "text",
                        "text": "Еда: доставка за N минут",
                        "font_size": 14,
                        "font_weight": "bold",
                        "font_style": "italic",
                        "color": "#000000"
                    }
                ]
              }
           },
          "show_policy": { // optional, временное решение, до того, как реализуем со стороны бэка mark-notify
                           // основная проблема данного решения - логика показа размазывается между бэкендом и клиентами, 
                           // информация о показе той или иной плашки теперь только из appmetrica
            "max_show_count": 3, // понятие сессии определяется клиентами (TODO - добавить позже в rfc)
            "max_widget_usage_count": 1, // количество действий считается по идентификатору промоплашки и сохраняется клиентами в локальном кэше
          }
        }
      ], // все промоблоки в рамках саммари
      "priority": [ // порядок промок в рамках выбранного тарифа
        {
          "class": "econom",
          "promoblocks_order": ["id1", "id2", "id3"] // офферы промоблоков, первый отображается под селектором тарифов, остальные при разворачивании карточки
        }
      ]
    }
  }
}
```

Основные продуктовые сценарии, которые ожидаются в MVP (и сразу после MVP):
- промоблок тарифа (курьер / доставка)
- промоблок яндекс.драйва

Что делать с текущими сценариями:
- конфликта по промоблоку быть не должно - ответ ручки занимает весь список промоблоков, 
все оставшиеся нотификации отдаваемые routestats отображаются по старым правилам (в нотификационном поп-апе)

### Приоритизация:
Для каждого промоблока в админке будет задан список тарифов, под которыми он может появиться (`supported_classes`). В экспериментах (консьюмер `inapp_communications/communications`) для промоблоков добавляем специальные кварги, отвечающие за матчинг тарифов. В качестве кваргов передаём тарифы из запроса, т.е. значение поля request.summary_state.tariff_classes.

Рассмотрим пример. Пусть некоторый промоблок (промоутирующий тариф `vip`) имеет следующие `supported_classes`: `econom`, `comfort`, `comfort+`. В эксперименте задан следующий `clause`:
```
{
  "predicate": {
    "init": {
      "predicates": [
        {
          "init": {
            "arg_name": "available_tariffs",
            "set_elem_type": "string",
            "value": "vip"
          },
          "type": "contains"
        }
      ]
    },
    "type": "any_of"
  },
  "title": "",
  "value": {
    "enabled": true
  }
}
```
Пусть в запросе следующий `summary_state.tariff_classes`: `["econom", "comfort", "vip", "ultima"]`.

Тогда эксперимент будет сматчен, т.к. summary_state.tariff_classes содержит тариф `vip`, промоблок будет показан в тех тарифах, которые попадают и в `supported_classes` из админки, и в `summary_state.tariff_classes`.

При этом на уровне inapp-communications поддержана логика, обеспечивающая полное совпадение классов из `summary_state.tariff_classes` и приходящих в ответе в `offers.promoblocks.priority`.

### Задачи:

### Клиентский флоу:
На данный момент предполагается вызов ручки сразу после вызова routestats клиентами. 
На стороне клиентов не указываются уже скаченные известные промоблоки, как это делалось для promotions, кэширование происходит только на уровне медиафайлов (image_tag'и / урлы изображений)

Что важно понимать:
- routestats не перезапрашивается при смене "selected_class" // Согласовано с @trygoginz - готовы перевыпустить клиентов, если понадобится такой функционал

*идея на будущее:* В дальнейшем, если мы захотим развивать идею с более гибким вызовом endpoint'а - думаю что core-ручка (routestats) должна будет возвращать policy для клиентов, 
которым будет регулироваться правила похода в коммуникацию - _в MVP не нужно_

**клиентский флоу по пунктам:**
1) поход в routestats и отображение классов / цен
2) поход в ручку промоблоками - (TODO: понять что клиенты отображают в этот момент)
3) загрузка медиаконтента только той плашки, которая отображается - отдельных стратегий предзагрузок пока не делаем

#### Этап 2 (+?)

- Реализация доп логики по "количеству показов" (аналогичная хотелка была/есть и у шорткатов)
- Добавление поддержки цен (предположительно через систему плагинов в routestats колбек на сохранение цен по offer_id)

### Как раскатываем

#### Раскатка этапа 1

1. Клиентский эксперимент в launch, который управляет логикой похода в ручку промоблоков после ответа routestats.
Почему не в routestats? Потому что предполагается что в каком-то светлом будущем routestats может быть распилен на несколько разных походов. 
Доступные кварги - стандартные в client_protocol/launch консьюмере.

{
    "name": "summary_promoblocks",
    "value": {
        "enabled": true,
    }
}
