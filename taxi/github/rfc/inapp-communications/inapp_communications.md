# Сервис для доставки клиентам in-app коммуникаций

## Бизнес-описание

В приложение есть разные виды коммуникаций (сторизы, фулскрины и т.д.) и
продолжают появляться новые(промо блоки). Нужно иметь возможность отдавать
клиенту подходящие ему коммуникации с небольшим latency (<3 сек). Так же хочется
иметь максимальную гибкость в настройке коммуникаций: когда, при каких действиях
клиента, каким группам пользователей показывать коммуникацию.

## Техническая реализация проекта

Коммуникации хранятся в существующей pg базе promotions.
Клиент при наступлении заданных событий ходит в новый сервис и запрашивает
все коммуникации, которые, возможно, нужно будет показать пользователю.
Сервис хранит все существующие коммуникации в кэше, который переодически обновляет,
ходя в ручку /internal/promotions/list сервиса promotions. При этом у сервиса promotions остается все
знание о внутренней структуре коммуникаций.
Логика выбора коммуникаций для отдачи клиенту:
1. Сервис собирает данные о клиенте, ходит в tags.
2. Коммуникации выбираются по 3-им экспериментам. Один эксперимент - одна коммуникация (есть исключения).
В кварги для матчинга экспериментов пробрасываются тэги висящие на пользователе,
(если применимо) параметры текущего заказа, текущее положение пользователя и
некоторая другая информация про пользователя. Также поддержана возможность передачи в кваргах дня недели и времени.
3. После отбора экспериментов, возможно, дополнительная фильтрация внутри сервиса.
4. Фильтруем коммуникации с помощью ML.

## Консьюмеры сервиса

В inapp-communications есть следующие консьюмеры:
1. inapp_communications/settings - общие для сервиса эксперименты (например, тогглы тех или иных фич)
2. inapp-communications/shortcuts-restaurants - см. описание ручки /4.0/inapp-communications/shortcuts
3. client_promotions/promotions_list - см. описание ручки /4.0/promotions/v1/list
4. Консьюмеры публикации коммуникаций (inapp_communications/communications, inapp_communications/promos_on_map, inapp_communications/promos_on_summary, inapp_communications/eda_communications, stories/stories, totw/promotions, promotions/list). Эксперименты этих консьюмеров служат для раскатки коммуникаций по экспериментам (альтернативный вариант - раскатка по YQL). Матч означает выдачу (при условии пропуска МЛем) данной коммуникации в ручке, мисматч - скип данной коммуникации в ручке. О том, по экспериментам каких консьюмеров матчатся те или иные коммуникации, можно почитать в описании к ручкам ниже.

### Ручки

#### POST /4.0/inapp-communications/communications
Ручка получает на вход состояние клиента. Отдавать ручка будет изменения в списке коммуникаций, которые должен показать клиент. Закладываемся сразу на diff, а не на все коммуникации, т.к. таких коммуникаций для клиента может быть очень много ~100.

Используемый для матчинга коммуникаций консьюмер - inapp_communications/communications.

Из кеша отдаём фуллскрины, нотификации, истории.

#### POST /4.0/inapp-communications/shortcuts
Главная задача ручки - агрегирование и приоритизация шорткатов (на данный момент шорткаты делятся на медиа-шорткаты и на диплинк-шорткаты). В процессе обработки шорткаты разделяются по scenario, и попадают в blender в разных классах. Сортировка в ML производится для ДШ и МШ вместе. Планируется гибкая сортировка, уникальная для данного scenario. В случае недоступности ML inapp-communications сортирует ДШ и МШ вместе в соответствии с приоритетом из админки.

Используемый для матчинга коммуникаций консьюмер - inapp_communications/communications. Также для построения кваргов ресторанов основного консьюмера применяется специальный консьюмер inapp-communications/shortcuts-restaurants.

Из кеша отдаём истории, диплинк-шорткаты, витрины.

Пример ответа:
```json
{
    "scenario_tops": [
        {
            "scenario": "media_stories",
            "shortcuts": [
                {
                    "content": {
                        "color": "#ffffff",
                        "text_color": "#21201f",
                        "title": "медиа для Саши"
                    },
                    "id": "0ec5d4cf0d71467eb0344d282e010100",
                    "scenario": "media_stories",
                    "scenario_params": {
                        "media_stories_params": {
                            "action_type": "media_stories",
                            "promo_id": "e5aa82f49aae46ba81d053c9ed823dd1:c5753c"
                        }
                    }
                }
            ]
        },
        {
            "scenario": "eats_block_other",
            "shortcuts": [
                {
                    "content": {
                        "color": "#558FC3",
                        "image_url": "https://taxi-promotions-testing.s3.mdst.yandex.net/73812a4d9a6d41cdb29b5af9d638553b.png",
                        "subtitle": "красные! 2",
                        "text_color": "#0C1E40",
                        "title": "Помидоры 2"
                    },
                    "id": "eaff9fa712f246509d441aa47eac2f47",
                    "scenario": "eats_block_other",
                    "scenario_params": {
                        "deeplink_params": {
                            "deeplink": "yandextaxi://external?service=grocery"
                        }
                    }
                },
                {
                    "content": {
                        "color": "#558FC3",
                        "image_url": "https://taxi-promotions-testing.s3.mdst.yandex.net/73812a4d9a6d41cdb29b5af9d638553b.png",
                        "subtitle": "красные!",
                        "text_color": "#0C1E40",
                        "title": "Помидоры"
                    },
                    "id": "1ee69a19fe8f4bed8d110f780ab60f36",
                    "scenario": "eats_block_other",
                    "scenario_params": {
                        "deeplink_params": {
                            "deeplink": "yandextaxi://external?service=grocery"
                        }
                    }
                }
            ]
        }
    ],
    "showcases": [
        {
            "blocks": [
                {
                    "cells": [
                        {
                            "one_of": [
                                {
                                    "scenario": "afisha_event",
                                    "type": "scenario"
                                },
                                {
                                    "tag": "sales",
                                    "type": "tag"
                                }
                            ],
                            "size": {
                                "height": 2,
                                "width": 2
                            }
                        },
                        {
                            "one_of": [
                                {
                                    "scenario": "afisha_event",
                                    "type": "scenario"
                                }
                            ],
                            "size": {
                                "height": 2,
                                "width": 2
                            }
                        }
                    ],
                    "name": "Пятница",
                    "slug": "collection_name"
                },
                {
                    "cells": [
                        {
                            "one_of": [
                                {
                                    "scenario": "1",
                                    "type": "scenario"
                                }
                            ],
                            "size": {
                                "height": 4,
                                "width": 2
                            }
                        },
                        {
                            "one_of": [
                                {
                                    "scenario": "2",
                                    "type": "scenario"
                                },
                                {
                                    "scenario": "fdsfs",
                                    "type": "scenario"
                                },
                                {
                                    "scenario": "fdsfdsf",
                                    "type": "scenario"
                                }
                            ],
                            "size": {
                                "height": 4,
                                "width": 4
                            }
                        }
                    ],
                    "name": "Monday",
                    "slug": "collection_1231"
                }
            ],
            "name": "showcase_name"
        }
    ]
}
```


#### POST /inapp-communications/v1/promos-on-map
Ручка получает на вход позицию и положение экрана пользователя. На выход отдаёт список коммуникаций на карте для пользователя. Ручка использует специальный pg-based кэш, в котором хранятся координаты коммуникаций на карте. Это было сделано во избежание "перепрыгиваний" коммуникации при изменении зума.

Используемый для матчинга коммуникаций консьюмер - inapp_communications/promos_on_map.

Из кеша отдаём промки на карте.

Пример запроса:
```json
{
    "position": [37.211375, 55.477065],
    "bbox": [37.211375, 55.477065, 38.022770, 55.983040],
    "cache_bbox": [37.211375, 55.477065, 38.022770, 55.983040],
    "location": [37.211375, 55.477065],
}
```

Пример ответа:
```json
{
    "objects": [
        {
            "id": "published_promo_on_map_id",
            "geometry": [37.56, 55.77],
            "image_tag": "image_tag2",
            "action": {
                "type": "show_screen_promo_action",
                "deeplink": "deeplink",
                "promotion_id": "promotion_id"
            },
            "bubble": {
                "id": "bubble_id",
                "hide_after_tap": true,
                "max_per_session": 1,
                "max_per_user": 10,
                "components": [{"type": "text", "value": "text on bubble"}]
            },
            "cache": {"distance": 1000}
        }
    ]
}
```

Политика выбора "action". 

1). В случае, если пользователь попал под эксперимент "deeplink_action_exp" и из promotions не был получен promotion_id, то type будет выставлен в "deeplink". В этом случае действие в layers будет распознано как DeeplinkAction.

2). В случае, если пользователь попал под эксперимент "deeplink_action_exp" и из promotions был получен promotion_id, то в качестве type будет указано "show_screen_promo_action". В этом случае действие в layers будет распознано как ShowScreenPromoAction.

3). В случае, если пользователь не попал под эксперимент "deeplink_action_exp" и из promotions был получен promotion_id, то в качестве type будет указано "show_screen_promo_action". Сервис layers распознает действие как ShowScreenPromoAction.

4). В случае, если пользователь не попал под эксперимент "deeplink_action_exp" и из promotions не был получен promotion_id, то промо-объект будет проигнорирован на стороне inapp-communications.

Сервис persuggest распознает действие как ShowScreenPromoAction в любом из случаев 1-3.

#### POST /inapp-communications/v1/eda-communications
Ручка, имеющая логику, схожую с /inapp-communications/v1/promos-on-map. В запросе поступает список объектов, доступных пользователю (касается ресторанов, брендов и коллекций), а также информация об ID устройства, о платформе и версии приложения. В соответствии с этой информацией ручка возвращает список баннеров, каждый из которых относится к одному из следующих типов: info, place, brand, collection.

Используемый для матчинга коммуникаций консьюмер - inapp_communications/eda_communications.

Из кеша отдаём баннеры еды.

Пример запроса:
```json
{
  "device_id": "string",
  "application": {
    "version": "0.0.0",
    "platform": "eda_desktop_web"
  },
  "state": {
    "point": {
      "latitude": 55.73552,
      "longitude": 37.642474
    },
    "places": [],
    "brands": [
      {
        "id": 24668
      }
    ],
    "collections": []
  }
}
```

Пример ответа:
```json
{
  "banners": [
    {
      "id": 66,
      "type": "info",
      "priority": 10,
      "url": "https://yandex.ru/promo/eda/tips",
      "app_url": "eda.yandex://webpage?title=%D0%97%D0%B0%D0%BA%D0%B0%D0%B7%20%D0%B4%D1%80%D1%83%D0%B3%D0%BE%D0%BC%D1%83&url=https%3A%2F%2Fyandex.ru%2Fpromo%2Feda%2Ftips",
      "description": "sdks",
      "payload": {
        "pages": [
          {
            "images": [
              {
                "url": "https://eda.yandex/images/1380157/a465b655c1b77fcd9962f6007d32dc4c.png",
                "theme": "light",
                "platform": "web"
              },
              {
                "url": "https://eda.yandex/images/1380157/a465b655c1b77fcd9962f6007d32dc4c.png",
                "theme": "dark",
                "platform": "web"
              },
              {
                "url": "https://eda.yandex/images/1380298/a3fa1be31e1fad7cb84625b5caca7509.png",
                "theme": "light",
                "platform": "mobile"
              },
              {
                "url": "https://eda.yandex/images/1380298/a3fa1be31e1fad7cb84625b5caca7509.png",
                "theme": "dark",
                "platform": "mobile"
              }
            ],
            "shortcuts": [
              {
                "url": "https://eda.yandex/images/1370147/d1898f97580fb2d2855e99ffbb23d350.png",
                "theme": "light",
                "platform": "mobile"
              },
              {
                "url": "https://eda.yandex/images/1370147/d1898f97580fb2d2855e99ffbb23d350.png",
                "theme": "dark",
                "platform": "mobile"
              }
            ]
          }
        ]
      }
    },
    {
      "id": 61,
      "type": "brand",
      "priority": 92,
      "brand_id": 24668,
      "description": "www",
      "payload": {
        "pages": [
          {
            "images": [
              {
                "url": "https://eda.yandex/images/1387779/bc54af81f78d9fe985072912f5b5640c.png",
                "theme": "light",
                "platform": "web"
              },
              {
                "url": "https://eda.yandex/images/1387779/bc54af81f78d9fe985072912f5b5640c.png",
                "theme": "dark",
                "platform": "web"
              },
              {
                "url": "https://eda.yandex/images/1368744/fd63117b7fd73b9609e27e96cf0278f7.png",
                "theme": "light",
                "platform": "mobile"
              },
              {
                "url": "https://eda.yandex/images/1368744/fd63117b7fd73b9609e27e96cf0278f7.png",
                "theme": "dark",
                "platform": "mobile"
              }
            ],
            "shortcuts": [
              {
                "url": "https://eda.yandex/images/1368744/44530fa6c7697fe611f545aebad4563b.png",
                "theme": "light",
                "platform": "mobile"
              },
              {
                "url": "https://eda.yandex/images/1368744/44530fa6c7697fe611f545aebad4563b.png",
                "theme": "dark",
                "platform": "mobile"
              }
            ]
          }
        ]
      }
    }
  ]
}
```

#### POST /4.0/promotions/v1/list

Ручка отдаёт список сматчившихся коммуникаций пользователю (при запуске приложения).

Используеме консьюмеры:
1. promotions/list для выдачи коммуникаций
2. client_promotions/promotions_list для выдачи typed_experiments (typed_experiments - клиентские эксперименты, для которых мы отдаём сам value (json) эксперимнета).

Из кеша отдаём баннеры фуллскрины, карточки, нотификации.

#### POST /4.0/promotions/v1/promotion/retrieve

Ручка отдаёт коммуникацию по запросу (фуллскрин, карточку, нотификацию или историю).

Используемых консьюмеров нет. Отдастся любая запрошенная коммуникация, если для неё найдётся (при необходимости) YQL-data или построится (при необходимости) attributed text.

Из кеша отдаём фуллскрины, карточки, нотификации и истории.

#### GET /3.0/getimage

Ручка возвращает путь до изображения для заданных tag, size, application.

Используемых консьюмеров нет.

Кеш не используется.

#### POST /4.0/inapp-communications/promos-on-summary

Ручка промо-объектов под саммари. Подробности в файле summary_promoblocks.md.
Коротко, схема следующая:
1. Сбор промоблоков с источников (в том числе и с самого inapp-communications по стандартному механизму матчинга экспериментов).
2. Отдача их в блендер для принятия решения о показе и порядке показа в том или ином тарифе. В случае недоступности блендера (или отключенном конфиге) сортировка происходит по id'шнику промоблоков.

Используемый для матчинга коммуникаций консьюмер - inapp_communications/promos_on_summary.

Из кеша отдаём т.н. промоблоки на саммари.

#### POST /inapp-communications/v1/promos-on-the-way

Ручка отдачи коммуникаций, получаемых в пути.

Используемый для матчинга коммуникаций консьюмер - totw/promotions.

Из кеша отдаём old-stories, totw-banners.

#### Базы данных

Сервис использует базу данных dbinappcommunications, используемая лишь для хранения координат промок на карте. Также временно (для получения YQL-data) сервис использует базу promotions. К сожалению, нет ничего более постоянного, чем временное.
