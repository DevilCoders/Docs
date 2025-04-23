# Проработка новых фулскринов
<!-- TOC -->

- [Проработка новых фулскринов](#проработка-новых-фулскринов)
    - [Проект в Стартреке](#проект-в-стартреке)
    - [Описание](#описание)
        - [Как работает сейчас](#как-работает-сейчас)
        - [Как будет работать](#как-будет-работать)
        - [YQL и объемы хранилища](#yql-и-объемы-хранилища)
        - [Подробности](#подробности)
    - [Взаимодействие с клиентами](#взаимодействие-с-клиентами)
        - [POST /4.0/promotions/v1/list](#post-40promotionsv1list)
            - [Ответ с фулскринами](#ответ-с-фулскринами)
            - [Ответ карточками](#ответ-карточками)
            - [Ответ с уведомлениями](#ответ-с-уведомлениями)
        - [POST /4.0/promotions/v1/promotion/retrieve](#post-40promotionsv1promotionretrieve)
            - [HTTP 200 OK](#http-200-ok)
            - [HTTP 400 Bad Request](#http-400-bad-request)
        - [Ручка для учета показанных коммуникаций](#ручка-для-учета-показанных-коммуникаций)
            - [POST /4.0/promotions/seen](#post-40promotionsseen)
    - [Изменения в админке](#изменения-в-админке)
        - [Список коммуникаций](#список-коммуникаций)
        - [Просмотр коммуникации](#просмотр-коммуникации)
        - [Загрузка медиа](#загрузка-медиа)
            - [Хранение картинок (медиа) с разными размерами](#хранение-картинок-медиа-с-разными-размерами)
            - [GET /admin/promotions/resize_modes/{media_type}.](#get-adminpromotionsresize_modesmedia_type)
            - [POST /admin/promotions/create_media_tag](#post-adminpromotionscreate_media_tag)
            - [POST /admin/promotions/upload](#post-adminpromotionsupload)
            - [POST /admin/promotions/autoresize](#post-adminpromotionsautoresize)
        - [Создание](#создание)
        - [Редактирование](#редактирование)
        - [Публикация](#публикация)
        - [Снятие с публикации](#снятие-с-публикации)
        - [Архивация](#архивация)
        - [Создание промо-объектов на карте](#создание-промо-объектов-на-карте)
        - [Редактирование промо-объектов на карте](#редактирование-промо-объектов-на-карте)
        - [Просмотр промо-объектов на карте](#просмотр-промо-объектов-на-карте)
        - [Публикация промо-объектов на карте](#публикация-промо-объектов-на-карте)
        - [Снятие с публикации промо-объектов на карте](#снятие-с-публикации-промо-объектов-на-карте)
        - [Архивация промо-объектов на карте](#архивация-промо-объектов-на-карте)
        - [Ручка тестовой раскатки](#ручка-тестовой-раскатки)
        - [Ручка со списком экспериментов](#ручка-со-списком-экспериментов)
    - [Межсервисное взаимодействие](#межсервисное-взаимодействие)
        - [Сервис taxi-admin-images](#сервис-taxi-admin-images)
            - [Как сервис работает сейчас](#как-сервис-работает-сейчас)
            - [Причины по которым было решено использовать taxi-admin-images](#причины-по-которым-было-решено-использовать-taxi-admin-images)
            - [Проблемы с текущим устройством сервиса](#проблемы-с-текущим-устройством-сервиса)
            - [Расширение и обобщение функционала сервиса в рамках задач promotions](#расширение-и-обобщение-функционала-сервиса-в-рамках-задач-promotions)
                - [Пример для ресайза по множителю](#пример-для-ресайза-по-множителю)
                - [Пример для ресайза по высоте экрана](#пример-для-ресайза-по-высоте-экрана)
            - [Про ресайз картинок в админке](#про-ресайз-картинок-в-админке)
            - [Как клиенты будут получать медиа](#как-клиенты-будут-получать-медиа)
    - [Мониторинги](#мониторинги)
    - [Декомпозиция задач и оценка](#декомпозиция-задач-и-оценка)
        - [I этап](#i-этап)
        - [II этап](#ii-этап)
        - [III этап](#iii-этап)

<!-- /TOC -->
## Проект в Стартреке
[TAXIPROJECTS-792](https://st.yandex-team.ru/TAXIPROJECTS-792)

## Описание
Сейчас фулскрины работают на экспериментах 2.0, запрашиваются клиентами,
выгружаются на устройства и отображаются при следующем запуске приложения.
Нужно уметь:
* выбирать большую аудиторию (до 20 млн. пользователей)
* делать рассылку коммуникаций по клиентам с определенным тегом (для скидок, например)
* массово рассылать пуши клиентам о появлении нового контента в /promotions
* забирать тексты из танкера
* подставлять в тексты переменные из YQL-таблиц
* таргетирование по типу приложения (эксперименты 3.0)
* realtime коммуникация (предположительно без графики)

### Как работает сейчас
Получаем все эксперименты 2.0 пользователя, ищем по этим экспериментам
фулскрин баннеры, добавляем найденное в список доступных баннеров (
минус те баннеры, которые пользователю уже показали – их список приходит в запросе).

### Как будет работать
Пишем новую ручку в API 4.0, которая
помимо показов коммуникаций нового формата, будет уметь показывать
старые в новом формате (конвертировать). Баннер будет показываться клиенту
единожды, после этого удаляться с устройства. Для текстовых полей (title, alt_title, text)
будет возможность указать, готовый ли это текст или ключ из танкера. В случае ключа,
при публикации бэкенд сходит в танкер и извлечет из него текст для подходящей локали
(придет в запросе или фолбек на английский). Если нет переводов для языка локали или анлийского, то коммуникация отдаваться не будет.
При указании ссылки на YQL-запрос, текст можно будет шаблонизировать.
В таком случае, при публикации бэкенд выполнит YQL-запрос и проведет все необходимые подстановки.
YQL-запрос и ключи из танкера можно комбинировать (в танкере находится шаблонизированный текст).
Второй способ сегментации аудитории (помимо YQL) – эксперименты 3.0 + теги.
Доступные атрибуты для экспериментов: os, version, app type, tags. Теги передаются
в эксперименты через предикат contains. Теги ассоциируются с пользователем через yandex_uid.
Все передаваемые изображения будут нарезаться по размерам из конфига и сохраняться в mds.
Бэкграунды типа видео и картинка возможны только у фулскринов. После релиза старая ручка поддерживаться не будет,
все новые коммуникации будут заводиться под новую ручку. 70% клиентов за 1-й месяц, 78% за 2 месяца, 80% за 3 месяца
и 85% за 6 месяцев обновляют свои приложения на новую версию.

### YQL и объемы хранилища
Предполагается, что данные из YQL будут выгружаться асинхронно (через stq-таску)
и сохраняться в БД на время действия коммуникации. Верхняя оценка аудитории в запросе YQL – 5 млн. записей.
Если предположить, что на запись будет приходиться 1 кб данных, то можно оценить объем
занимаемого хранилища в БД приблизительно в 5 Гб. По прикидкам менеджеров, таких
объемных коммуникаций будет не больше одной единовременно. Доступный объем хранилища на старте – 100 Гб.

### Подробности
Разработка микросервиса на py3. Ожидается, что будет порядка нескольких сотен одновременно активных
коммуникаций. Чтобы не показывать клиенту одну и ту же коммуникацию больше одного раза, будет сделана
ручка `/4.0/promotions/v1/seen`, в которой будут фиксироваться просмотренные пользователем коммуникации.
Дополнительно, ручка `/4.0/promotions/v1/list` будет отдавать заголовки `Cache-Control` и `Last-Modified`, чтобы
снизить количество входящих запросов.

## Взаимодействие с клиентами
Клиенты будут дергать новую ручку в том же режиме,
в котором дергают старую: при каждом запуске приложения и раз каждые 4 часа.
Дополнительно, iOS-клиенты могут запросить ручку при получении silent-пуша; также
в iOS есть механизм, позволяющий приложениям докачивать данные.

### POST /4.0/promotions/v1/list

```json
{
  "banners_seen": ["22b83dec2d5dcd69854231f63d27d046", "8263d27dcd423ec22b8dd5d351f69046"],
  "size_hint": 280,
  "media_size_info": {
    "screen_height": 1920,
    "screen_width": 1080,
    "scale": 2.5
  },
  "supported_types": ["fullscreen_banners", "cards", "notifications"],
  "supported_widgets": ["close_button", "menu_button", "switch_button", "arrow_button", "link", "action_buttons"],
  "supported_background_types": ["video", "image", "color", "lottie"],
  "supported_features": ["markdown"]
}
```

По данным:
{
  "size_hint": 280,
  "media_size_info": {
    "screen_height": 1920,
    "screen_width": 1080,
    "scale": 2.5
  },
}
Подбираем размеры всех требуемых медиа.

#### Ответ с фулскринами
```json
{
  "fullscreen_banners": [
    {
      "id": "5cc0e8eb0c69ff1a8a364b37",
      "zones": ["abakan"],
      "screen": "pickup_location",
      "start_date": "2019-05-13T21:00:00.0000Z",
      "end_date": "2019-06-30T20:59:00.0000Z",
      "priority": 1,
      "pages": [
        {
          "title": {
            "content": "Заголовок",
            "color": "bc23af",
          },
          "alt_title": {
              "content": "Альтернативный заголовок",
              "color": "bc23af",
          },
          "text": {
            "content": "Некоторый текст, занимающий, желательно не более {count} строк",
            "color": "bc23af",
          },
          "image": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
          "backgrounds": [
            {
              "type": "video",
              "content":  "/static/video/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
            },
            {
              "type": "image",
              "content": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
            },
            {
              "type": "color",
              "content": "ff02bc"
            }
          ],
          "widgets": {
            "close_button": {
                "color" : "bc23af"
            },
            "link": {
                "text": "Хочу узнать больше",
                "text_color": "afbc23",
                "deeplink": "yandextaxi://deeplink"
            },
            "action_buttons": [{
                "color" : "bc23af",
                "text": "Отмена",
                "text_color": "afbc23",
                "deeplink": "yandextaxi://deeplink"
            }],
            "pager": {
                "color_on": "fa0bed",
                "color_off": "fa0bed"
            }
          }
        },
        {
          "title": {
            "content": "Заголовок 2",
            "color": "bc23af",
          },
          "alt_title": {
              "content": "Альтернативный заголовок 2",
              "color": "bc23af",
          },
          "text": {
            "content": "Некоторый текст, занимающий, желательно не более {count} строк",
            "color": "bc23af",
          },
          "image": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
          "backgrounds": [
            {
              "type": "video",
              "content":  "/static/video/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
            },
            {
              "type": "image",
              "content": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
            },
            {
              "type": "color",
              "content": "ff02bc"
            }
          ],
          "widgets": {
            "close_button": {
                "color" : "bc23af"
            },
            "action_buttons": [
              {
                "color" : "bc23af",
                "text": "Спасибо",
                "text_color": "afbc23",
                "deeplink": "yandextaxi://deeplink"
              },
              {
                "color" : "bc23af",
                "text": "Отмена",
                "text_color": "afbc23",
                "deeplink": "yandextaxi://deeplink"
              }
            ]
          }
        }
      ]
    },
    {
      "pages": [{}, {}, {}]
    }
  ]
}
```


#### Ответ карточками
```json
{
  "cards": [
    {
      "title": {
        "content": "Заголовок",
        "color": "bc23af",
        "type": "(large|small)",
      },
      "alt_title": {
        "content": "Альтернативный заголовок 2",
        "color": "bc23af",
      },
      "text": {
        "content": "Некоторый текст, занимающий, желательно не более {count} строк",
        "color": "bc23af",
      },
      "icon": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
      "image": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
      "is_foldable": true,
      "backgrounds": [
        {
          "type": "color",
          "content": "ff02bc"
        }
      ],
      "widgets": {
        "link": {
            "text": "Хочу узнать больше",
            "text_color": "afbc23",
            "deeplink": "yandextaxi://deeplink"
        },
        "action_buttons": [{
            "color" : "bc23af",
            "text": "Хорошо",
            "text_color": "afbc23",
            "deeplink": "yandextaxi://deeplink"
        }]
      },
      "id": "5cc0e8eb0c69ff1a8a364b37",
      "zones": ["abakan"],
      "screen": "pickup_location",
      "start_date": "2019-05-13T21:00:00.0000Z",
      "end_date": "2019-06-30T20:59:00.0000Z"
    }
  ]
}
```


#### Ответ с уведомлениями
```json
{
  "notifications": [
    {
      "title": {
        "content": "Поездка будет оплачена картой",
        "color": "ff12ee",
      },
      "text": {
        "content": "MasterCard ****5005",
        "color": "ff12ee",
      },
      "icon": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
      "widgets": {
        "switch_button": {
          "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
          "color_on": "fa0bed",
          "color_off": "fa0bed",
          "text": "Отмена",
          "text_color": "afbc23"
        },
        "arrow_button": {
          "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
          "color": "afafaf",
          "text": "Хорошо"
        }
      },
      "id": "5cc0e8eb0c69ff1a8a364b37",
      "zones": ["abakan"],
      "screen": "pickup_location",
      "start_date": "2019-05-13T21:00:00.0000Z",
      "end_date": "2019-06-30T20:59:00.0000Z"
    }
  ]
}
```

### POST /4.0/promotions/v1/promotion/retrieve
```json
{
  "promotion_id": "<promotion_id>",
  "size_hint": 280,
  "supported_types": ["fullscreen_banners", "cards", "notifications"],
  "supported_widgets": ["close_button", "menu_button", "switch_button", "arrow_button", "link", "action_buttons"],
  "supported_background_types": ["video", "image", "color", "lottie"],
  "supported_features": ["markdown"]
}
```
Ручка для получения опубликованного баннера по его promotion_id. Если промка неопубликована или не найдена – вернется HTTP 400. Форматы промок в ответах такие же, как и в ручке списка + дополнительное поле `promotion_type`.

#### HTTP 200 OK
```json
{
  "id": "5cc0e8eb0c69ff1a8a364b37",
  "promotion_type": "(fullscreen|card|notification)",
  "title": {
    "content": "Заголовок",
    "color": "bc23af",
    "type": "(large|small)",
  },
  "alt_title": {
    "content": "Альтернативный заголовок 2",
    "color": "bc23af",
  },
  "text": {
    "content": "Некоторый текст, занимающий, желательно не более {count} строк",
    "color": "bc23af",
  },
  "icon": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
  "image": "/static/images/38292/035fbc0f-5cab-48a7-abbf-c437ab9d362f",
  "is_foldable": true,
  "backgrounds": [
    {
      "type": "color",
      "content": "ff02bc"
    }
  ],
  "widgets": {
    "link": {
        "text": "Хочу узнать больше",
        "text_color": "afbc23",
        "deeplink": "yandextaxi://deeplink"
    },
    "action_buttons": [{
        "color" : "bc23af",
        "text": "Хорошо",
        "text_color": "afbc23",
        "deeplink": "yandextaxi://deeplink"
    }]
  },
  "zones": ["abakan"],
  "screen": "pickup_location",
  "start_date": "2019-05-13T21:00:00.0000Z",
  "end_date": "2019-06-30T20:59:00.0000Z"
}
```

#### HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Коммуникация не найдена"
}
```

### Ручка для учета показанных коммуникаций
Черновик запроса

#### POST /4.0/promotions/seen
```json
{
  "seen_at": "2019-09-25T12:33:04.0000Z",
  "communication_id": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
  "user_action": "close_button"
}
```
Привязываемся к yandex_uid'у, как к правильному идентификатору пользователя.

## Изменения в админке
Ручки для админки предполагается делать в этом же сервисе и подключить их
через админку без кода.
Нужны ручки для:
* списка коммуникаций
* просмотр одной коммуникации
* загрузки медиа
* создания
* редактирования (только до публикации)
* публикации
* снятия с публикации
* архивирования
* создания/редактирование/просмотра промо-объектов на карте
* публикации промо-объектов на карте
* снятия с публикации промо-объектов на карте
* архивирования промо-объектов на карте

### Список коммуникаций
GET /admin/promotions/list/?type=fullscreen&name=Merry%20Xmas&show_archived=true&offset=10&limit=10
Возвращает список всех промоушенов. Есть возможность пагинации через
параметры  `offset` и `limit`.

Доступные фильтры:
* `type` – по типу коммуникации
* `name` – поиск по подстроке в имени
* `status` – по статусу коммуникаций (по умолчанию выводится все, кроме архивированных)

Ответ 200 OK
```json
{
  "items": [
    {"id": "598db7ac72ab36f85f9de70f", "name": "banner 1"},
    {"id": "598db7ac72ab36f85f9de71f", "name": "banner 2"},
    {"id": "598db7ac72ab36f85f9de72f", "name": "banner 3"},
    {"id": "598db7ac72ab36f85f9de73f", "name": "banner 4"}
  ],
  "total": 25,
  "offset": 21,
  "limit": 10
}
```

### Просмотр коммуникации
GET /admin/promotions/?promotion_id=5cc0e8eb0c69ff1a8a364b38

Ответ 200 OK
Для фулскрина
```json
{
  "id": "5cc0e8eb0c69ff1a8a364b38",
  "created_at": "2019-05-13T21:00:00.0000Z",
  "updated_at": "2019-05-13T21:00:00.0000Z",
  "published_at": "2019-05-13T21:00:00.0000Z",  // только для опубликованных
  "is_published": false,
  "name": "fullscreen name",
  "promotion_type": "fullscreen",
  "experiment": "all_moscow_comfort_plus",
  "ticket": "TAXIRATE-20",
  "pages": [{
    "title": {  // может отсутствовать
      "content": "Title",
      "color": "ff12ee",
      "is_tanker_key": false // может отсутствовать
    },
    "alt_title": {  // может отсутствовать
      "content": "Альтернативный аголовок 2",
      "color": "bc23af",
      "is_tanker_key": false // может отсутствовать
    },
    "text": {  // может отсутствовать
      "content": "MasterCard ****5005",
      "color": "ff12ee",
      "is_tanker_key": false // может отсутствовать
    },
    "image": {
      "id": "<media_tag>",
      "type": "image",
      "resize_mode": "height_fit",
      "sizes": [
          {"field": "original", "value":0, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":640, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1080, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1440, "mds_id": "<uuid4>", "url": "<url>"},
      ]
    },
    "icon": {
      "id": "<media_tag>",
      "type": "image",
      "resize_mode": "height_fit",
      "sizes": [
          {"field": "original", "value":0, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":640, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1080, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1440, "mds_id": "<uuid4>", "url": "<url>"},
      ]
    },
    "backgrounds": [
      {
        "id": "<media_tag>",
        "type": "image",
        "resize_mode": "height_fit",
        "sizes": [
            {"field": "original", "value":0, "mds_id": "<uuid4>", "url": "<url>"},
            {"field": "screen_height", "value":640, "mds_id": "<uuid4>", "url": "<url>"},
            {"field": "screen_height", "value":1080, "mds_id": "<uuid4>", "url": "<url>"},
            {"field": "screen_height", "value":1440, "mds_id": "<uuid4>", "url": "<url>"},
        ]
      },
      {
        "id": "<media_tag>",
        "type": "video",
        "resize_mode": "original_only",
        "sizes": [
            {"field": "original", "value":0, "mds_id": "<uuid4>", "url": "<url>"},
        ]
      },
      {"type": "color", "content": "ff02bc"}
    ],
    "widgets": {
      "action_buttons": [{
          "color" : "bc23af",
          "text": "Отмена",
          "text_color": "afbc23",
          "deeplink": "yandextaxi://deeplink"
      }],
      "switch_button": {
        "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
        "color_on": "fa0bed",
        "color_off": "fa0bed",
        "text": "\\u041e\\u0442\\u043c\\u0435\\u043d\\u0430",
        "text_color": "afbc23"
      },
      "arrow_button": {
        "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
        "color": "afafaf",
        "text": "\\u0425\\u043e\\u0440\\u043e\\u0448\\u043e"
      },
      "pager": {
          "color_on": "fa0bed",
          "color_off": "fa0bed"
      }
    }
  }],
  "zones": [
    "abakan"
  ],
  "screen": "pickup_location",
  "start_date": "2019-05-13T21:00:00.0000Z",
  "end_date": "2019-06-30T20:59:00.0000Z"
}
```

Для карточки
```json
{
  "id": "5cc0e8eb0c69ff1a8a364b38",
  "created_at": "2019-05-13T21:00:00.0000Z",
  "updated_at": "2019-05-13T21:00:00.0000Z",
  "published_at": "2019-05-13T21:00:00.0000Z",
  "is_published": true,
  "name": "card communication name",
  "promotion_type": "card",
  "experiment": "all_moscow_comfort_plus",
  "ticket": "TAXIRATE-20",
  "pages": [{
    "title": {  // может отсутствовать
      "content": "My title",
      "color": "ff12ee",
      "type": "(large|small)",  // только для карточки
      "is_tanker_key": false // может отсутствовать
    },
    "alt_title": {  // может отсутствовать
      "content": "Альтернативный заголовок 2",
      "color": "bc23af",
      "is_tanker_key": false // может отсутствовать
    },
    "text": {  // может отсутствовать
      "content": "MasterCard ****5005",
      "color": "ff12ee",
      "is_tanker_key": false // может отсутствовать
    },
    "image": {
      "id": "<media_tag>",
      "type": "image",
      "resize_mode": "height_fit",
      "sizes": [
          {"field": "original", "value":0, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":640, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1080, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1440, "mds_id": "<uuid4>", "url": "<url>"},
      ]
    },
    "icon": {
      "id": "<media_tag>",
      "type": "image",
      "resize_mode": "height_fit",
      "sizes": [
          {"field": "original", "value":0, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":640, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1080, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1440, "mds_id": "<uuid4>", "url": "<url>"},
      ]
    },
    "is_foldable": true,  // только для карточки
    "widgets": {
      "switch_button": {
        "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
        "color_on": "fa0bed",
        "color_off": "fa0bed",
        "text": "\\u041e\\u0442\\u043c\\u0435\\u043d\\u0430",
        "text_color": "afbc23"
      },
      "arrow_button": {
        "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
        "color": "afafaf",
        "text": "\\u0425\\u043e\\u0440\\u043e\\u0448\\u043e"
      }
    }
  }],
  "zones": [
    "abakan"
  ],
  "screen": "pickup_location",
  "start_date": "2019-05-13T21:00:00.0000Z",
  "end_date": "2019-06-30T20:59:00.0000Z"
}
```

Для нотификации
```json
{
  "id": "5cc0e8eb0c69ff1a8a364b38",
  "created_at": "2019-05-13T21:00:00.0000Z",
  "updated_at": "2019-05-13T21:00:00.0000Z",
  "published_at": "2019-05-13T21:00:00.0000Z",
  "is_published": false,
  "name": "fullscreen name",
  "promotion_type": "notification",
  "experiment": "all_moscow_comfort_plus",
  "ticket": "TAXIRATE-20",
  "pages": [
    {
    "title": {  // у нотификаций не бывает alt_title, может отсутствовать
      "content": "My title",
      "color": "ff12ee",
      "is_tanker_key": false // может отсутствовать
    },
    "text": {  // может отсутствовать
      "content": "MasterCard ****5005",
      "color": "ff12ee",
      "is_tanker_key": false // может отсутствовать
    },
    "icon": {
      "id": "<media_tag>",
      "type": "image",
      "resize_mode": "height_fit",
      "sizes": [
          {"field": "original", "value":0, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":640, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1080, "mds_id": "<uuid4>", "url": "<url>"},
          {"field": "screen_height", "value":1440, "mds_id": "<uuid4>", "url": "<url>"},
      ]
    },
    "widgets": {
      "switch_button": {
        "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
        "color_on": "fa0bed",
        "color_off": "fa0bed",
        "text": "\\u041e\\u0442\\u043c\\u0435\\u043d\\u0430",
        "text_color": "afbc23"
      },
      "arrow_button": {
        "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
        "color": "afafaf",
        "text": "\\u0425\\u043e\\u0440\\u043e\\u0448\\u043e"
      }
    }
  }],
  "zones": [
    "abakan"
  ],
  "screen": "pickup_location",
  "start_date": "2019-05-13T21:00:00.0000Z",
  "end_date": "2019-06-30T20:59:00.0000Z"
}
```

### Загрузка медиа

Медиа -- термин, под которым подразумеваем картинки, видео или еще какой-нибудь контент.
Для загрузки медиа во время [создания комумникации](#создание) или [редактирования](#редактирование) существующей коммуникации есть два сценария:

- Меди еще не загружено. Тогда:
  1. Создать *media_tag* c помощью ручки /create_media_tag
  2. Загрузить по новому *media_tag* картинку в самом большом размере (оригинал) с помощью ручки upload.
  3. (по выбору) Сделать авторесайз с помощью ручки /autoresize.
    Применимо не ко всем видам медиа, что учтено в поле resize_mode.

- Если изображение уже загружено, значит *media_tag* уже создан, значит к нему нужно\
прикрепить изображение с определенным размером с помощью ручки upload.\
Так же может быть доступен авторесайз.

#### Хранение картинок (медиа) с разными размерами
На данный момент поддерживается 4 способа хранения размеров (resize_mode):

- **scale_factor** - хранение по множителю, например 2X, 1.5X, 4X.
- **height_fit** - хранение по высоте экрана, например 720, 1080, 1440.
- **width_fit** - хранение по ширине экрана, например 480, 640, 720.
- **original_only** - опция для хранения только файла оригинального качества (размера).

#### GET /admin/promotions/resize_modes/{media_type}.

Ручка возвращает конфиг для выбранного media_type (image|video) способы хранения (resize_mode).

Ответ 200 OK
```json
{
  "scale_factor": [
    {"field": "original", "value":0}, // Есть для любого типа хранения медиа
    {"field": "scale", "value":1},
    {"field": "scale", "value":2},
    {"field": "scale", "value":2.5}
  ],
  "height_fit": [
    {"field": "original", "value":0},
    {"field": "screen_height", "value":640},
    {"field": "screen_height", "value":1080},
    {"field": "screen_height", "value":1440}
  ],
  "width_fit": [
    {"field": "original", "value":0},
    {"field": "screen_width", "value":320},
    {"field": "screen_width", "value":640},
    {"field": "screen_width", "value":720}
  ],
  "original_only": [ // Есть для любого типа медиа
    {"field": "original", "value":0}
  ],
}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Конфиг для данного тип меда не найден"
}
```

#### POST /admin/promotions/create_media_tag

В админке promotions предполагается следующий паттерн создания media_tag:
```javascript
  `promotions_${uuid4()}`
```
Пример: "promotion_7e388ac3-745d-423c-9e4c-bdd0dc4f1625"

Запрос
```json
{
  "type": "image|video",
  "id": "promotion_7e388ac3-745d-423c-9e4c-bdd0dc4f1625",
  "resize_mode": "scale_factor|width_fit|height_fit|original_only",
}
```

Ответ 200 OK
```json
{
  "media_tag": "promotion_7e388ac3-745d-423c-9e4c-bdd0dc4f1625"
}
```

#### POST /admin/promotions/upload

Ручка сохраняет файл в MDS и прикрепляет его к структуре media_tag.

POST /admin/promotions/upload/\
Content-Type: multipart/form-data\
Поля запроса:
- media_tag_id -- куда будем прикреплять загружаемый медиа
- content -- медиафайл
- field=screen_height (поле из media_size_info на которое мы смотрим при отдаче картинки)
- value = 640 (значение выше указанного поля, при котором мы отдаем отосланную картинку)

Вместе field и value однозначно идентифицируют размер картинки в рамках одно resize_mode
однозначно идентифицирует записываемый размер.

Ответ 200 OK
```json
{
  "id": "<mds_id>",
  "url": "<url>"
}
```

#### POST /admin/promotions/autoresize

В данный момент ресайз и загрузка картинок осуществлена в этом сервисе.\
В планах переехать на хранение картинок через сервис [taxi-amdin-images](#сервис-taxi-amdin-images).

Для ресайза нужен media_tag, в котором в качестве resize_mode выбран один из вариантов:
- **scale_factor** - ресайз по множителю, например 2X, 1.5X, 4X.\
  Для загрзки требуется картинка с самым большим доступным размером из конфига (сейчас это X4).
  Об этом нужно **обязательно** предупредить пользователя чем-нибудь очень жирным и заметным.
- **height_fit** - ресайз по высоте экрана, например 720, 1080, 1440.\
  Для загрузки требуется картинка с высотой >= самой большой высоте экрана из конфига.
  Об этом так же нужно сказать пользователю.
- **width_fit** - ресайз по ширине экрана, например 480, 640, 720.\
  Для загрузки требуется картинка с шириной >= самой большой ширнине экрана из конфига.
  Об этом так же нужно сказать пользователю.

Для ресайза используется картинка, которая хранится по размеру:
{"field": "original", value:0}
Это так называемая оригинальная картинка, требуем ее большой, чтобы ресайзить только в меньшую сторону.

Запрос
```json
{
  "media_tag": "<media_tag>"
}
```

Ответ 200 OK

Ответ HTTP 400 Bad Request
```json
{
  "code": "autoresize_impossible",
  "message": "Авторесайз для resize_mode: 'original_only' невозможен."
}
```


### Создание
POST /admin/promotions/create/
```json
{
  "name": "Some new cool banner",
  "promotion_type": "fullscreen",
  "zones": ["moscow", "abakan"],
  "screen": "main",
  "priority": 123,
  "pages": [
    {
      "title": {
        "content": "content",
        "color": "ff12ee",
        "is_tanker_key": false // может отсутствовать
      },
      "text": {
        "content": "MasterCard ****5005",
        "color": "ff12ee",
        "is_tanker_key": false // может отсутствовать
      },
      "image": {
        "type": "image",
        "id": "<media_tag>"
      },
      "icon": {
        "type": "image",
        "id": "<media_tag>"
      },
      "backgrounds": [
        {
          "type": "image",
          "id": "<media_tag>"
        },
        {
          "type": "image",
          "id": "<media_tag>"
        },
        {
          "type": "image",
          "id": "<media_tag>"
        },
      ],
      "widgets": {
        "switch_button": {
          "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
          "color_on": "fa0bed",
          "color_off": "fa0bed",
          "text": "\\u041e\\u0442\\u043c\\u0435\\u043d\\u0430",
          "text_color": "afbc23"
        },
        "arrow_button": {
          "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
          "color": "afafaf",
          "text": "\\u0425\\u043e\\u0440\\u043e\\u0448\\u043e"
        }
      }
    },
  ]
}
```

Ответ HTTP 201 Created
```json
{
  "id": "5cc0e8eb0c69ff1a8a364b39",
  "name": "Some new cool banner",
  "promotion_type": "fullscreen"
}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "already_exists",
  "message": "Коммуникация с таким названием уже существует",
  "details": {"reason": "Reason here"}  // необязательное поле
}
```

### Редактирование

Комментарий к загрузке картинок:
Редактирование структуры *sizes* в коммуникации (promotion) не перезаписывает картинки в базе.
Поменять картинку для конкретного размера можно только в [POST /admin/promotions/upload/](#ресайз-картинок-при-загрузке).
Это сделано для обратной совместимости с текущим клиентом.
Если изменилась картинка только для конкретного размера, нужно прокинуть в поле id (media_tag) прежнее значение.
Поле sizes передавать не обязательно.

PUT /admin/promotions/{promotion_id}/
```json
{
  "name": "Some new cool banner",
  "promotion_type": "fullscreen",
  "zones": ["moscow", "abakan"],
  "screen": "main",
  "priority": 123,
  "pages": [
    {
      "title": {
        "content": "content",
        "color": "ff12ee",
        "is_tanker_key": false // может отсутствовать
      },
      "text": {
        "content": "MasterCard ****5005",
        "color": "ff12ee",
        "is_tanker_key": false // может отсутствовать
      },
     "image": {
        "type": "image",
        "id": "<image_tag>",
      },
      "icon": {
        "type": "image",
        "id": "<image_tag>"
      },
      "backgrounds": [
        {
          "type": "image",
          "id": "<image_tag>"
        },
      ],
      "widgets": {
        "switch_button": {
          "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
          "color_on": "fa0bed",
          "color_off": "fa0bed",
          "text": "\\u041e\\u0442\\u043c\\u0435\\u043d\\u0430",
          "text_color": "afbc23"
        },
        "arrow_button": {
          "deeplink": "https://plus.yandex.ru/card?utm_source=taxi&utm_medium=cpc&utm_campaign=fullscreen",
          "color": "afafaf",
          "text": "\\u0425\\u043e\\u0440\\u043e\\u0448\\u043e"
        }
      }
    },
  ]
}
```
Редактировать можно только неопубликованные коммуникации.

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "edit_error",
  "message": "Нельзя редактировать опубликованные коммуникации",
  "details": {"reason": "Reason here"}  // необязательное поле
}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "already_exists",
  "message": "Коммуникация с таким названием уже существует",
  "details": {"reason": "Reason here"}  // необязательное поле
}
```

Ответ HTTP 404 Not Found
```json
{
  "code": "not_found",
  "message": "Коммуникация не найдена",
  "details": {"reason": "Reason here"}  // необязательное поле
}
```

### Публикация
POST /admin/promotions/publish/
```json
{
  "promotion_id": "promotion_id",
  "experiment": "exp3_name",
  "yql_link": "https://yql.yandex-team.ru/Operations/<query_id>",
  "start_date": "2019-05-13T21:00:00.0000Z",
  "end_date": "2019-05-13T21:00:00.0000Z",
  "ticket": "STTICKET-123123"
}
```
При публикации необходимо указать либо `experiment`, либо `yql_link`.
Если указать оба поля, то `yql_link` имеет больший приоритет.

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Коммуникация не найдена"
}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "data_missing",
  "message": "Необходимо указать эксперимент или YQL-ссылку"
}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "already_published",
  "message": "Коммуникация уже опубликована"
}
```

### Снятие с публикации
POST /admin/promotions/unpublish/
```json
{
  "promotion_id": "promotion_id"
}
```

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Коммуникация не найдена"
}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "not_published",
  "message": "Коммуникация еще не опубликована"
}
```

### Архивация
POST /admin/promotions/archive/
```json
{
  "promotion_id": "promotion_id"
}
```

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Коммуникация не найдена"
}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "already_published",
  "message": "Невозможно архивировать опубликованную коммуникацию"
}
```

### Создание промо-объектов на карте
POST /admin/promo_on_map/create/
```json
{
  "name": "promo_on_map",
  "priority": 1,
  "image_tag": "image_tag",
  "action": {
    "deeplink": "yandextaxi://route?level=119",
    "promotion_id": "82e49bb9d56240cfa6d9ee9acb25cff6"
  },
  "bubble": {
    "id": "cargo_promo_bubble",
    "components": [
      {
        "type": "text",
        "value": "object.cargo.bubble",
        "font_style": "italic",
        "is_tanker_key": false
      }
    ],
    "max_per_user": 1000,
    "hide_after_tap": false,
    "max_per_session": 1000
  },
  "cache_distance": 1000,
  "attract_to_road": true
}
```

Ответ HTTP 201 Created
```json
{
  "id": "fce6de0e9de54de4928202aecc67f3db",
  "name": "promo_on_map"
}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "already_exists",
  "message": "Промо-объект с таким названием уже существует"
}
```

### Редактирование промо-объектов на карте
PUT /admin/promo_on_map/{promo_on_map_id}/
```json
{
  "name": "promo_on_map",
  "priority": 1,
  "image_tag": "image_tag",
  "action": {
    "deeplink": "yandextaxi://route?level=119",
    "promotion_id": "82e49bb9d56240cfa6d9ee9acb25cff6"
  },
  "bubble": {
    "id": "cargo_promo_bubble",
    "components": [
      {
        "type": "text",
        "value": "object.cargo.bubble",
        "font_style": "italic",
        "is_tanker_key": false
      }
    ],
    "max_per_user": 1000,
    "hide_after_tap": false,
    "max_per_session": 1000
  },
  "cache_distance": 1000,
  "attract_to_road": true
}
```

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "edit_error",
  "message": "Нельзя редактировать опубликованные промо-объекты"
}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "already_exists",
  "message": "Промо-объект с таким названием уже существует"
}
```

Ответ HTTP 404 Not Found
```json
{
  "code": "not_found",
  "message": "Промо-объект не найден"
}
```

### Просмотр промо-объектов на карте
GET /admin/promo_on_map/?promotion_id=fce6de0e9de54de4928202aecc67f3db

Доступные фильтры:
* `promotion_id` – поиск по id

Ответ HTTP 200 OK
```json
{
  "id": "fce6de0e9de54de4928202aecc67f3db",
  "name": "promo_on_map",
  "priority": 1,
  "image_tag": "image_tag",
  "action": {
    "deeplink": "deeplink",
    "promotion_id": "promotion_id"
  },
  "bubble": {
    "id": "bubble_id",
    "hide_after_tap": true,
    "max_per_session": 1,
    "max_per_user": 10,
    "components": [
      {
        "type": "text",
        "value": "text on bubble",
        "is_tanker_key": false
      }
    ]
  },
  "created_at": "2019-07-22t16:51:09.000000Z",
  "updated_at": "2019-07-22t16:57:09.000000Z",
  "status": "created",
  "cache_distance": 1000,
  "attract_to_road": true
}
```

### Публикация промо-объектов на карте
POST /admin/promo_on_map/publish/
```json
{
  "promotion_id": "promo_on_map_id",
  "experiment": "cargo_object_on_map",
  "start_date": "2019-05-13T21:00:00.0000Z",
  "end_date": "2019-05-13T21:00:00.0000Z"
}
```

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Промо-объект не найден"
}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "already_published",
  "message": "Промо-объект уже опубликован"
}
```

### Снятие с публикации промо-объектов на карте
POST /admin/promo_on_map/unpublish/
```json
{
  "promotion_id": "promo_on_map_id"
}
```

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Промо-объект не найден"
}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "not_published",
  "message": "Промо-объект еще не опубликован"
}
```

### Архивация промо-объектов на карте
POST /admin/promo_on_map/archive/
```json
{
  "promotion_id": "promo_on_map_id"
}
```

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Промо-объект не найден"
}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "already_published",
  "message": "Невозможно архивировать опубликованный промо-объект"
}
```

### Ручка тестовой раскатки
Принадлежность номеров к Яндексу или Такси будет обеспечиваться одним из условий эксперимента.
Промки будут публиковаться на ограниченное время, по умолчанию 1 час от момента запроса — этот
промежуток будет управляться конфигом `PROMOTIONS_TEST_PUBLISH_TIME_RANGE_MINUTES`.
Доступность фичи будет определяться конфигом `PROMOTIONS_TEST_PUBLISH_ENABLED`.
Имя эксперимента будет задаваться конфигом `PROMOTIONS_TEST_PUBLISH_EXP_NAME`

POST /admin/promotions/test_publish
```json
{
  "promotion_id": "<promotion_id>",
  "phones": ["+79991234567", "+79997654321"]
}
```

Ответ HTTP 200 OK
```json
{}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "not_found",
  "message": "Коммуникация не найдена"
}
```

Ответ HTTP 400 Bad Request
```json
{
  "code": "test_publish_disabled",
  "message": "Тестовая публикация отключена"
}
```

Ответ HTTP 409 Conflict
```json
{
  "code": "already_published",
  "message": "Коммуникация уже опубликована"
}
```

### Ручка со списком экспериментов
Возвращает список включенных экспериментов консьюмера `promotions/list`.

GET /admin/promotions/experiment_list

Ответ HTTP 200 OK
```json
{
  "experiments": ["one", "two", "three"]
}
```

## Межсервисное взаимодействие

### Сервис taxi-admin-images
Для хранения картинок с разными размерами будет использоваться сервис taxi-admin-images,
но есть больше планы на расширение его фунцкиоанала, который может пригодиться не только в сервисе promotions.

#### Как сервис работает сейчас
Картинки в макетах дизайнеров задаются в некоторых абстрактных единицах для **Android** это *dp*, для **IOS** это *point*.
Эти абстрактные единцы получают физический смысл (значение в пикселях) когда они умножаются на некоторый множитель устройства.
Множитель определяется по плотности пикселей на дюйм экрана (dpi) и потому не лишен недостатков,
например если у двух устройств одинаковый dpi, а разрешение разное.\
Множителям сопоставили идентификаторы на каждой из платформ,
требуемый множитель стали отправлять в запросе через поле *size_hint* в сервис.\
Сейчас для каждого *size_hint* маркетологи/менеджеры загружают картинки в соответствии с размером руками.

В сервисе все картинки собраны в группы которым дали human readable идентификатор -- image_tag.\
Для одного image_tag сопоставлен список пар (size_hint, id картинки в MDS).\
id, по которому хранится картинка в MDS, соответствует по размеру *size_hint* из пары.

#### Причины по которым было решено использовать taxi-admin-images
1. В сервисе есть логика хранения картинок с разными размерами.
2. Есть возможность перезаписывать картинку с определенным size_hint в рамках одного image_tag.
3. Это отдельный сервис и если нам пришлют картинку от которой будет корка, сервис promotions продолжит работу для клиентов. (Например картинка с zip-бомбой.)
4. Переиспользоваие taxi-admin-images позволит другим сервисам не создавать своего клиента для хранения картинок. К тому же для этих потенциальных сервисов-пользователей уже готовы view в админке.

#### Проблемы с текущим устройством сервиса

1. Одному и тому же size_hint соответствуют разные размеры экранов.
   - Это стало актуально когда в promotions появились картинки на весь экран.
2. Все размеры картинок загружаются вручную.
3. Ресайз доступен только по множителю.
4. Для автоматического ресайза в существующем клиенте недостаточно информации.
   - Для рейсайза под разные множители нам нужно знать с каким множителем нам загружают картинку.
5. Сервис работает только с одним namespace в MDS, использование которого сильно повысит на него нагрузку.
6. Сервис предназначен только для хранения картинок.
   - Есть требование к хранению и ресайзу видео, хранению векторных картинок.
7. Ручки сервиса предназначены для использования админкой. Нет кодогенерируемого клиента или сервиса.


  Следовательно, нужно уметь хранить размеры картинок не по плотности, а например по высоте экрана.

#### Расширение и обобщение функционала сервиса в рамках задач promotions

Что касается хранения контента, предполагается следующая структура:

##### Пример для ресайза по множителю
```json
{
  "<media_tag>": {
    "media-type": "image", // image|video|vector
    "mds_id": "<uuid4>",
    "resize_mode": "scale_factor", // scale_factor|height_fit|width_fit|original_only
    "sizes": [
      {"field": "original", "value":0, "mds_id": "<uuid4>"}
      {"field": "scale", "value":1, "mds_id": "<uuid4>"},
      {"field": "scale", "value":1.5, "mds_id": "<uuid4>"},
      {"field": "scale", "value":2, "mds_id": "<uuid4>"}
    ]
  }
}
```

##### Пример для ресайза по высоте экрана
```json
{
  "<media_tag>": {
    "media-type": "image", // image|video|vector
    "mds-id": "<uuid4>",
    "resize_mode": "height_fit", // scale_factor|height_fit|width_fit|original_only
    "sizes": [
      {"field": "original", "value":0, "mds_id": "<uuid4>"}
      {"field": "screen_height", "value":640, "mds_id": "<uuid4>"},
      {"field": "screen_height", "value":1080, "mds_id": "<uuid4>"},
      {"field": "screen_height", "value":1440, "mds_id": "<uuid4>"}
    ]
  }
}
```


#### Про ресайз картинок в админке

В рамках задачи [TAXIBACKEND-25351](https://st.yandex-team.ru/TAXIBACKEND-25351)
в сервисе taxi-admin-images планируется добавление автоматического ресайза картинок (и не только картинок).
Потому опишу общий вариант добавления медиа через админку.

Алгоритм действий человека, загружающего картинку в админку:
  1. Выбрать бакет в MDS в котором будет хранится картинка.
  2. Выбрать тип контента: картинка, видео, вектор.
  3. Определить нужен ли ресайз для картинки.
     1. Если нужен то переключить бегунок ресайза.
     1. Выбрать способ ресайза: по множителю, по высоте экрана, по ширине экрана.
     2. Посмотреть в появившемся списке доступных размеров самый большой размер.
     3. Загрузить картинку с размером, соответствующим самому большому из списка, по кнопке "загрузить".
  4. Сохранить медиа.
  5. После успешного сохранения можем получить media_tag картинки.
  6. Если производился ресайз, проверить картинки на наличие артефактов/искажений изображения.
  7. Для изображений где у конкретных размеров нашлись искажений перезагрузить картинки отдельно с помощью кнопки загрузки напротив нужного размера.

Про свойства ресайза:
 - Ресайз будет происходит только в сторону уменьшения, потому картинка должна быть достаточно большой.
 - Для scale_factor будет Огромный Warning что загружаем с максимальным доступным масштабом и указываем этот масштаб.
 - Для height_fit, width_fit если не соответствует по высоте/ширине, клиент не дает загрузить такую картинку.
 - Ресайзить в рамках одного media_tag можно только одним способом.

#### Как клиенты будут получать медиа

**Сейчас** клиенты присылают нам size_hint причем в разных местах он разный (взято из [вики](https://wiki.yandex-team.ru/taxi/mobile-taxi-images/)):

IOS, ручка getimage, картинки class_*_poi:
 - size_hint=128 -- 2x
 - size_hint=192 -- 3x

IOS, ручка zoneinfo, картинки class_*_car*, class_*_icon* и другие:
 - size_hint=206 -- 2x
 - size_hint=240 -- 2x
 - size_hint=300 -- 3x
 - size_hint=390 -- 3x

IOS, promotions:
- size_hint=высота экрана в пикселях

Android, все картинки:
 - size_hint=120 -- 0.75x
 - size_hint=160 -- 1x
 - size_hint=240 -- 1.5x
 - size_hint=320 -- 2x
 - size_hint=480 -- 2.5x
 - size_hint=640 -- 3x

Т.к. нужно поддерживать и старые версии клиента, для обратной совместимости будет добавлено сопоставление *size_hint* - (width, hight, scale). С помощью него будут мигрированы картинки из taxi-admin-images и старой коллекции картинок promotions. Т.к. в promotions *size_hint* для IOS передается высота экрана, то для них
мы будет отдавать картинку с самым большим размером
*size_hint=min(sent_size_hint, max_size_hint)*.


В для получения **новых медиа** клиенты будут присылать структуру:
```json
{
  "media_size_info": {
    "screen_height": 1920,
    "screen_width": 1080,
    "scale": 1.5
  }
}
```

И по этим данным мы будем отдавить url картинки нужного размера в зависимости от того,
какой способ ресайза для него заводили в админке.

## Мониторинги
* количество активных коммуникаций
* количество публикуемых в настоящее время коммуникаций
* количество зафейленных при публикации

## Декомпозиция задач и оценка
Общая задача бэкенда со всеми подзадачами – [TAXIBACKEND-23122](https://st.yandex-team.ru/TAXIBACKEND-23122)

### I этап
* [TAXIBACKEND-23123](https://st.yandex-team.ru/TAXIBACKEND-23123) – микросервис и стаб (2d)
* [TAXIBACKEND-23124](https://st.yandex-team.ru/TAXIBACKEND-23124) – конвертация старых коммуникаций (2d)
* [TAXIBACKEND-23142](https://st.yandex-team.ru/TAXIBACKEND-23142) – используем сегментацию по exp3.0 + tags (2d)
* [TAXIBACKEND-23125](https://st.yandex-team.ru/TAXIBACKEND-23125) – отдача новых коммуникаций (1d 4h)
* [TAXIBACKEND-23209](https://st.yandex-team.ru/TAXIBACKEND-23209) – учет показа коммуникаций (2d)
* [TAXIBACKEND-23659](https://st.yandex-team.ru/TAXIBACKEND-23659) – моки ручек админки (2d)
* [TAXIBACKEND-23630](https://st.yandex-team.ru/TAXIBACKEND-23630) – dry-run, проверка нагрузки (2d)
Приблизительное окончание этапа – 1 неделя августа

### II этап
* [TAXIBACKEND-23128](https://st.yandex-team.ru/TAXIBACKEND-23128) – проработка API админки (1d 2h)
* [TAXIBACKEND-23129](https://st.yandex-team.ru/TAXIBACKEND-23129) – реализация API админки (2d)
* [TAXIBACKEND-23634](https://st.yandex-team.ru/TAXIBACKEND-23634) – отдаем cards + notifications (1d)
* [TAXIBACKEND-23126](https://st.yandex-team.ru/TAXIBACKEND-23126) – используем ключи из Танкера в текстовых полях (2d)
* [TAXIBACKEND-23631](https://st.yandex-team.ru/TAXIBACKEND-23631) – мониторинги и алерты (2d)
Приблизительное окончание этапа – конец августа

### III этап
* [TAXIBACKEND-23127](https://st.yandex-team.ru/TAXIBACKEND-23127) – используем сегментацию по YQL (тут же шаблонизация) (7d)
* [TAXIBACKEND-23632](https://st.yandex-team.ru/TAXIBACKEND-23632) – очистка временных данных (yql подстановки) (2d)
* [TAXIBACKEND-23130](https://st.yandex-team.ru/TAXIBACKEND-23130) – отправка пушей через Xiva (2d)
Приблизительное окончание этапа – вторая половина сентября
