### Internal promoblocks source
**Запрос:** 
```json5
{
    "summary_state": {
        "offer_id": "some_offer_id", // идентификатор, которые позволит в будущем выгрузить цены
        "tariff_clasess": ["econom", "vip"] // список тарифов доступных пользователю (из ответа routestats), required: true
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
       }
   },
  "client_info": {
      "supported_features": [
        {"type": "promoblock", "widgets": ["arrow_button"]}
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
  "offers": { 
    "promoblocks": {
      "items":  [
         {
          "id": "5cc0e8eb0c69ff1a8a364b37",
          "meta_type": "drive_promo_block", // добавлен относительно внешнего ответа, предлагаю использовать для метаинформации в блендере
          "supported_classes": ["econom"], // добавлен, относительно внешнего ответа
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
    }
  }
}
```

### Promoblocks-Blender

**Запрос:** 
```json5
{

    "request_info": { // весь клиентский запрос
        "summary_state": {
            "offer_id": "some_offer_id", // идентификатор, которые позволит в будущем выгрузить цены
            "tariff_clasess": ["econom", "vip"] // список тарифов доступных пользователю (из ответа routestats), required: true
        },
        "state": {
           "location": [lon, lat],
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
           }
       },
        "client_info": {
          "supported_features": [
            {"type": "promoblock", "widgets": ["arrow_button"]}
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
    "offers": { 
    "promoblocks": {
      "items":  [
        ... // такой же, как ответ интернал ручки source, но при этом объединенный от всех source'ов
      ]
    },
   }
}
```

**Ответ:** 
```json5
{
      "priority": [ // порядок промок в рамках выбранного тарифа
        {
          "class": "econom",
          "promoblocks_order": ["id1", "id2", "id3"] // офферы промоблоков, первый отображается под селектором тарифов, остальные при разворачивании карточки
        }
      ]
}
```