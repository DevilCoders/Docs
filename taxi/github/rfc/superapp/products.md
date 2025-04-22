## Бизнесовая задача

### Описание

Уметь показывать пользователям "шорткаты" с подготовленными для пользователя сценариями использования Такси, Еды и Лавки.

### Гипотеза

Необходимо поднять количество заказов в Лавке до 500 в день. Предполагается, что шорткаты это эффективный способ достичь данной метрики (не все понимают что такое "Лавка", не все хотят там что-то искать, шорткаты экономят клики и предлагают пользователю персонализированные сценарии)

## Дизайн

![Shortcuts](https://jing.yandex-team.ru/files/privet/shortcuts.png "Шорткаты")

Фигма: https://www.figma.com/file/YtgPLmshzweePUMctcQWuz/Шорткаты

### Клиентское API

(описание бекенда ниже)

Ручка `4.0/mlutp/v1/products`. Из запроса и ответа можно выкидывать поля, если
1) мы в них не уверены
2) они не нужны для шорткатов
3) их можно будет добавить позже

```
POST /4.0/mlutp/v1/products

{
   "position": [lon, lat], // pin position
   "supported_vertical_types": ["group"],  // as in /zoneinfo
   "shortcuts": {
    "supported_actions": [
        {"type": "deeplink"},
        {"type": "taxi:summary-redirect",  "destination_support": true},
        // при destination_support=true внутри "action" могут быть проброшены поля "uri", "position", "log"
        // это обусловнено необходимостью задавать конечную точку из источника шортката,
        // в частности, узнавать точку Б напрямую из оффера драйва из сервиса persuggest вместо того,
        // чтоб брать её из /4.0/persuggest/v1/zerosuggest
        {"type": "discovery", "modes": ["drive", "masstransit"]},
        {"type": "taxi:route-input"},
    ],
    "supported_sections": [
        { "type": "header_linear_grid" },
        { "type": "items_linear_grid" },
        { "type": "buttons_container" }
    ],
    "multicolor_service_icons_supported": true, // optional, default: false. see `colored_service_icons.md`
    "supported_icon_sizes": [
        "medium",
        "big"
    ],
    "supported_features": [ // No shortucts if shortcuts.supported_features is not sent
        { 
            "type": "taxi:header-summary-redirect",
            "prefetch_strategies": []
        },
        { 
            "type": "taxi:route-input",
            "prefetch_strategies": []
        },
        {
            "type": "eats-based:superapp",
            "prefetch_strategies": [],
            "services": ["eats", "grocery", "pharmacy"]
        },
        { 
            "type": "header-deeplink",
            "prefetch_strategies": []
        },
        {
            "type": "taxi:expected-destination",
            "prefetch_strategies": ["routestats", "route_eta"]
            # routestats - поход в routestats за eta и ценой
            # route_eta - поход в /4.0/mlutp/route-matrix за временем в пути
        },
        {
            "type": "deeplink",
            "prefetch_strategies": []
        },
        {
            "type": "media-stories",
            "prefetch_strategies": ["disable_media", "images", "all_media"]
            # disable_media - предзагружает метаинформацию по промоушенам, но без медиафайлов
            # images - предзагружает метаинформацию + картинки
            # all_media - предзагружает все медиафайлы
        },
        {
            "type": "header-action-driven",
            "prefetch_strategies": []
            # для кирпичиков, action которых содержит type [из supported_actions]
        },
        {
            "type": "action-driven",
            "prefetch_strategies": []
            # для шорткатов, action которых содержит type [из supported_actions]
        }
    ]
      "mdash_width": 20.0,
      "ndash_width": 9.0,
      "grids_support": [
         {
            "width": 6,
            "unit_width": 100.0,
         }
      ]
   }
   "state": {
       "appearance_mode": <mode>, // "default", "ultima", "sdc", "drive"
       "selected_class": <class>, // "econom", "comfort", ...
       "multiclass_options": {
           "class": [
             "econom",
             "comfortplus",
             "vip"
           ],
           "selected": true
         },
       "location": [lon, lat]
       "accuracy": ...,
       "bbox": [ 37.615, 55.758, 37.619, 55.753 ],
       "known_orders": [   // not required for mvp
           "taxi:<taxi_order_id>:revision", // revision from totw
           "eats:<eats_order_id>",  // maybe not needed now
           "grocery:<grocery_order_id>" // maybe not needed now
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
  "media_size_info": {
    "screen_height": 1920,
    "screen_width": 1080,
    "scale": 2.5
  }
}
```

Response
```json
{
    "modes": [
        {
            "mode": "taxi",
            "layout": {
                "grid_id": "some_id",  // blender identifier
                "type": "linear_grid", // aka SuperApp V2
                "width": 6, // in units
            },
            "offers": {
                "header": [
                    {
                        "shortcut_id": "...",
                        "any shortcut from supported_features could be used": ""
                    }
                ],
                // Кладу шорткаты в items чтобы была возможность докинуть в корень какую-то метаинформацию
                "items": [  // Какие офферы/шорткаты показывать. Подробнее ниже
                    {
                        "shortcut_id": ..., // id of shortcut from shortcut provider
                        "title": "Some title",
                        "subtitle": "Some subtitile",
                        "background": {
                            # при наличии и image_tag и image_url -
                            # image_url приоритетнее
                            "image_tag": ..., # optional
                            "image_url": ..., # optional
                            "color": ...
                        },
                        "overlays": [
                            {
                                "text": "до 5л",
                                "text_color": "#00",
                                "background": {
                                    "color": "#fff"
                                },
                                "image_tag": "some-tag-for-poi",
                                "shape": "sticker|bubble|poi"  // allowed shapes depend on shortcut type
                            }
                        ],
                        "width": 2, // possible values based on figma: 2, 3, 4
                        "height": 1, // hardcoded value for MVP
                        "type": "deeplink|taxi:expected-destination"
                        "action": {
                            "deeplink": ...
                        },
                    },
                    { ... }  // см. API шорткатов для примеров по Еде/Лавке
                ]
            }
        },
        {
            "mode": "eats"
            // "see_products_availabile.md"
        }
    ],
    // Не будет отдано сейчас т.к. не используется
    "products": [
        // "see_products_availabile.md"
    ]
}
```

Важно: отправка полей `appearance_mode`, `selected_class`, `multiclass_options` в `v1/products` не должна зависеть от ответов других сервисов (ex. `personalstate`). Изменение этих полей по любым причинам (смена тарифа, геозоны, местоположение пина) должно триггерить новый вызов `v1/products`.

#### Про appearance_mode

Поле `appearance_mode` продуктово используется для отрисовки шторы ультимы. Цель поля: дать бекенду понять, что пользователь находится в режиме "ultima", и для него требуется соответствующая кастомизация UI. Изначально поле называлось `current_mode` (аналогично `*suggest*` ручкам), однако в процессе реализации оказалось что возможные значения `current_mode` включают в себя не только значения `zoneinfo.modes`, но и дополнительные. Для решения этой проблемы поле переименовали.

#### API шорткатов

Речь идет про часть `modes.mode=taxi.offers`.
Хочется уметь показывать шорткаты как в фигме https://www.figma.com/file/YtgPLmshzweePUMctcQWuz/Шорткаты

Шорткат — это панелька, по нажатию на которую что-то происходит. В мвп есть такие шорткаты:
1) "Такси" — по нажатию происходит переход на саммари с адресом из саджеста (какой элемент саджеста должен быть выбран — должен сообщит бекенд)
1) "Еда" — по нажатию открывается карточка ресторана.
1) "Лавка" — по нажатию открывается карточка ресторана.
1) "Инвайты" - по нажатию открывается карточка инвайтов пользователя для приглашения в закрытый клуб

Потенциально в будущем могут появиться:
* открытие последнего заказа по шорткату еды/лавки
* шорткаты для других сервисов
* фулскрины
* ???

Итого, клиенту нужно знать
1) Последовательность отображения шорткатов
1) Статичные параметры отображения (текст, картинка, цвет фона...)
1) Их размеры (частично это параметр отображения, но стоит выделить отдельно)
1) Действие по нажатию

Имхо, про поля `title`, `subtitle`, `background` все понятно. Интересные части:

`width`

Сколько места занимает шорткат на сетке. Размеры сетки указаны в `modes.mode=taxi.layout.width`. В будущем может появиться регулирование высоты шорткатов.

`type`

Влияет на обработку нажатия на шорткат (фактически, какие поля должны интересовать клиента в `action`)
1) deeplink — по нажатию должен открыться диплинк `action.deeplink`

Пример для открытия определенного ресторана в Еде:
```
    "type": "deeplink"
    "title": "МакДональдс",
    "subtile": "Хочешь заточить чизон?"
    "background": {
        "image_tag": "superchizon",
        "color": "#aaffaa"
    },
    "width": 2,
    "height": 1,
    "action": {
        "deeplink": "yandextaxi://external?service=eats&href=restaurants/coffemania-sadovnicheskaya"
    },
```

Шаблон диплинка: "yandextaxi://external?service=eats&href=restaurant/{restaraunt_slug}}"

Пример для открытия определенной категории в определенной Лавке:

```
    "type": "deeplink"
    // ...generic display fields..
    "action": {
        "deeplink": "yandextaxi://external?service=grocery&href=restaurant/produkty_kamenshhiki?category=32961"
    },
```

Шаблон диплинка: "yandextaxi://external?service=grocery&href=restaurant/{lavka_slug}?category={category_id}"


2) taxi:expected-destination — по нажатию должен открыться саммари с геобъектом из саджеста

Пример:
```
    "type": "taxi:expected-destination",
    "title": "Дом",
    ...generic display fields..
    "action": {
        "position": [...], // from zerosuggest
        "log": "ymapsbm1://geo?otherlog=parameter&ll=37.637%2C55.732&spn=0.001%2C0.001&...",  // from zerosuggest
        "uri": "ymapsbm1://geo?ll=37.637%2C55.732&spn=0.001%2C0.001&...",  // from zerosuggest
        "prefetch": "routestats|route_eta" # регулирует логику подгрузки цены и eta (routestats - ходим в routestats, нужные поля подставляем, route_eta - ходим в ручку /4.0/mlutp/route-matrix, поля нет - не ходим никуда)
    },
```

3) media — по нажатию должен открываться промоутирующий материал - клиенты могут предзагружать его по правилам, описанным в prefetch для media-stories

Пример:
```
    "background": {
      "color": "#FCF0A8",
      "image_url": "…"
    },
    ...
    "type": "media-stories",
    "action": {
      "prefetch: "disable_media|images|all_media", # регулирует логику загрузки media (promotions_retrieve - предзагружаем, отсутствие поля - нет)
      "media": {
           "promo_id": "100500"
       }
    },

```

4) invites - инвайты для вступления в закрытый клуб

Источник - сервис `invites`, ручка `/invites/v1/shortcuts`
Проработка ручки https://github.yandex-team.ru/taxi/rfc/pull/271/files

Пример:
```
    ...
    "title": "Позвать 5 друзей",
    "type": "invites",
    "width": 2,
    "height": 4,
    "text_style": {
      "color": "#FFFFFF" // Цвет для текста в title и subtitle шортката
    },
    "background": {
      "color": "#75736F"
    },
    "action": {
      "title_text": "Показать друзьям Go",
      "body_text": "Вот вам пять волшебных ссылок, которые превращают Яндекс.Такси в Яндекс Go.",
      "confirm_button_text": "Согласен",
      "invites": [
        {
          "code": "dk482ndlz",
          "button_text": "Ссылка для друга №1",
          "share_text": "Что у нас там yandextaxi://activateinvite?code=dk482ndlz",
          "status": "new"
        },
        {
          "code": "38vksoxj3",
          "button_text": "Ссылка для друга №2",
          "share_text": "Что у нас там yandextaxi://activateinvite?code=38vksoxj3",
          "status": "activated"
        }
      ]
    }
    ...
```

5) taxi:route-input

Контрол ввода маршрута. Бекенд явно сообщает "размер" инпута на сетке, заголовок и иконку

```json
{
    "title": "Куда едем?",
    "type": "taxi:route-input",
    "icon_tag": "taxi_route_input_tag",
    "width": 3,
    "height": 1,
    "background": {
        "color": "#F1F0ED"
    }
}
```
6) header-deeplink

Диплинки для шапки — рисуются по правилам динамических кирпичиков, при нажатии переход по диплинку

```json
{
    "title": "Доставка",
    "type": "header-deeplink",
    "width": 3,
    "height": 1,
    "background": {
        "color": "#F1F0ED"
    },
    "action": {
        "deeplink": "yandextaxi://route?level=50"
    }
}
```

В ближайшем будущем планируется использовать для MVP Доставки и QR-кодов

7) eats-based:superapp

Осуществляет открытие шторки "работающей по протоколу Еды" через диплинк. На примере Лавки:

```json
{
    "title": "Lavka",
    "type": "eats-based:superapp",
    "width": 3,
    "height": 1,
    "service": "grocery",
    "icon_tag": "grocery_icon_tag",
    "background": {
        "color": "#F1F0ED"
    },
    "action": {
        "deeplink": "yandextaxi://external?service=grocery",
    }
}
```


8). drive:fixpoint-offers

Осуществляет переход в режим дискавери и редирект на самую подходящую машинку драйва.

9). taxi:header-summary-redirect

Редирект на саммари (используется для кирпичика "Доставка").

10). header-action-driven

Кнопки и кирпичики с таким типом исполняют `action` любого типа. С бека приходят только `actions`, имеющие поле `type`.

11). action-driven

Шорткат с таким типом исполняет `action` любого типа. С бека приходят только `actions`, имеющие поле `type`. Клиенты умеют обрабатывать `overlays` любого типа для данного типа шорткатов. Пример для редиректного шортката драйва (при `destination_support=true` в запросе):
```json
{
    "title": "Домой",
    "subtitle": "на Драйве",
    "type": "action-driven",
    "background": {
        "color": "#F1F0ED"
    },
    "text_style": {
        "color": "#9e9b98"
    },
    "overlays": [
        {
            "image_tag": "drive_shortcut_car_poi",
            "shape": "poi"
        },
        {
            "image_tag": "drive_shortcut_car_tag",
            "shape": "car"
        }
    ],
    "action": {
        "vertical": "drive",
        "class": "drive",
        "state": "collapsed",
        "type": "taxi:summary-redirect",
        "vertical_trap": true,
        "destination": {
            "position": [...],
            "log": "ymapsbm1://geo?otherlog=parameter&ll=37.637%2C55.732&spn=0.001%2C0.001&...",
            "uri": "ymapsbm1://geo?ll=37.637%2C55.732&spn=0.001%2C0.001&..."
        }
    }
}
```


Список возможных сервисов ограничивается через значения из `supported_features.["type"=="eats-based:superapp"].services`

 Конечный внешний вид кирпичика зависит от его размеров и доступных свойств, определяется на клиенте.

#### Оверлеи

`overlays`

Механизм добавления дополнительных элементов. Примеры — бейджи на шорткатах еды и стикеры на шорткатах лавки.
Оверлей интерпретируется клиентом в зависимости типа шортката. На данный момент бекенд не управляет расположением оверлея, т.к. это требует изобретения системы разметки внутри шортката (нужно управлять вертикальным и горизонтальным положением и углом наклона), и пока что мы можем ограничиться строгими правилами расположения на клиентах для каждого сочетания {shortcut_type:overlay_shape}

* `shape=badge|sticker`

Для шорткатов с типом `deeplink`. Клиент рисует графику из shape в левом углу, располагает в нем текст из `.text` с цветом `.text_color`, цвет фона определяется через `.background.color`

* `shape=poi`

Для шорткатов с типом `taxi:expected-destination`. Клиент рисует графику в правой части (окружность с тенью) с цветом `.background.color`. В центр помещается картинка из `.image_tag`.

* `shape=car`

В нижнем левом углу отрисовывается картинка из `.image_tag`.

Для шорткатов с типом `action-driven` поддержана отрисовка оверлеев всех возможных `shape`. 

## Архитектура бекенда

Высокоуровневая архитектура лежит здесь: https://wiki.yandex-team.ru/taxi/backend/product-team-2/shortkaty/
