# Инфраструктура сториз в Еде

### Общая часть
#### 1. Описание RFC
В RFC описывается бэкенд для cториз в приложение Еды.

Описано использование двух сервисов:
* бэкенд админки (сервис feeds-admin): API для админки и запись актуальных сториз в feeds
* база данных сообщений (сервис feeds): отдача сторих по запросу от API Еды, их подготовка при необходимости (локализация, подстановка ссылок на медиа-ресурсы)

В RFC не описаны:
* продуктовые сервисы, отвечающие на клиентское API и бизнес-логику
* дизайн сториз в приложении
* UI админки

__Расположение в админке:__
Яндекс.Еда -> Коммуникации, Вкладка "Коммуникации в приложении".
В дальнейшем сюда можно добавить вкладки других видов коммуникаций.

__Дизайн админки:__
Похож на https://tariff-editor.taxi.tst.yandex-team.ru/promotions.
Немного отличается редактор сториз и настройки аудитории. Макеты будут приложены к тикету на фронт.

#### 2. Существующие решения
В Такси сториз обслуживаются сервисом `promotions`. Этот сервис в процессе миграции: API админки переезжает в сервис `feeds-admin`, база данных сообщений - в сервис `feeds`, клиентские ручки и логика - в сервис `inapp-communications`.
Поэтому сториз в еде решили делать сразу на основе `feeds-admin` + `feeds`

#### 3. Процесс работы со сториз
* Редактор создает во фронте админке сториз. Фронт сохраняет параметры сториз в feeds-admin.
* Редактор публикует через админку сториз, указывая период публикации, название эксперимента и тикет. Фронт дергает ручку публикации в feeds-admin.
* feeds-admin в указанное время передает сториз в сервис feeds.
* Продуктовое API запрашивает в feeds сториз, указывая в запросе id пользователя и названия экспериментов.
* Продуктовое API может пометить сториз прочитанной/удаленной запросом в feeds. Это логируется в YT.
* Редактор может дострочно снять сториз с публикации. Фронт дергает ручку снятия с публикации в feeds-admin.


#### 4. Описание payload
payload - это контент сториз, передаваемый между фронтом и бэкендом админки.
Он преобразуется перед тем как будет отдан в продуктовое API:
* вместо media_id будут подставлены реальные URL
* вместо ссылок на танкерные ключи будут подставлены строки на нужно языке

Формат payload должен быть совместимым с форматом сториз в такси чтобы можно было использовать один и тот же фреймворк на клиенте.

```javascript
{
    "is_tapable": true,
    "mark_read_after_tap": true,

    // Превью
    "preview": {
        "text": {
            "color": "FFFFFF",
            "content": "Недели Италии"
        },

        "title": {
            "color": "FFFFFF",

            // Локализуемое сообщение.
            // Перед отправкой в клиентское API будет заменено на
            // "content": "Переведенный текст".
            "content": {
                "keyset": "eda_client",
                "key": "translate_me"
            }        
        },

        "backgrounds": [
            {
                // В media_id значение, которое возвращает ручка /v1/media/upload.
                // Перед отправкой в клиентское API будет заменено на
                // "content": "https://..."
                "type": "image",
                "media_id": "3f30427b198b4d56be1aecaf73c83597"
            },
            {
                "type": "color",
                "content": "6D131C"
            }
        ]
    },

    // Список слайдов
    "pages": [
        {
            "autonext": true,
            "duration": 15,

            "text": {
                "color": "FCE381",
                "content": "text"
            },
            "title": {
                "color": "FFCF6A",
                "content": "header"
            },

            // Массив фонов в порядке он наименее приоритетного до самого приоритетного.
            // Пока клиент не загрузит более приоритетный, должен отображать менее приоритетный.
            // Должно быть указано два фона: color + один из (image, video, animation).
            "backgrounds": [
                {
                    "type": "color",
                    "content": "FFCF6A"
                },
                {
                    "type": "image",
                    "media_id": "3f30427b198b4d56be1aecaf73c83597"
                },
                {
                    "type": "video",
                    "media_id": "4f30427b198b4d56be1aecaf73c83597"
                },
                {
                    "type": "animation",
                    "media_id": "5f30427b198b4d56be1aecaf73c83597"
                }
            ],

            // Массив виджетов. Все виджеты опциональны.
            "widgets": {
                // Кнопка закрытия story
                "close_button": {
                    "color": "21201f"
                },

                // Переключатель слайдов
                "pager": {
                    "color_on": "FFCF6A",
                    "color_off": "EA503F"
                },

                // Кнопка открытия меню 
                "menu_button": {
                    "color": "FFCF6A"
                },

                // Ссылка.
                // Тип и контент ссылок аналогичен action_buttons
                "link": {
                    "text": "Текст ссылки",
                    "action": {
                        "type": "deeplink",
                        "payload": {
                            "content": "https://google.com",
                            "need_authorization": true
                        }
                    },
                    "text_color": "FFCF6A"
                },

                // Кнопки действий.
                // Массив т.к. их может быть несколько.
                "action_buttons": [
                    // Кнопки с диплинком
                    {
                        "text": "Кнопки с диплинком",
                        "color": "FFCF6A",
                        "text_color": "FFCF6A",
                        "action": {
                            "type": "deeplink",
                            "payload": {
                                "content": "https://yandex.ru",
                                "need_authorization": true
                            }
                        }
                    },

                    // Кнопка перехода на i'ую страницу
                    {
                        "text": "Кнопка перехода на i'ую страницу",
                        "text_color": "FFCF6A",
                        "color": "FFCF6A",
                        "action": {
                            "type": "move",
                            "payload": {
                                "page": "3",
                                "need_authorization": true
                            }
                        }
                    },

                    // Кнопка "поделиться"
                    {
                        "text": "Кнопка поделиться",
                        "text_color": "FFCF6A",
                        "color": "FFCF6A",
                        "action": {
                            "type": "share",
                            "payload": {
                                "content": "https://yandex.ru",
                                "need_authorization": true
                            }
                        }
                    },

                    // Кнопка, открывающая web view
                    {
                        "text": "Кнопка, открывающая web view",
                        "text_color": "EBAE41",
                        "color": "FFCF6A",
                        "action": {
                            "type": "web_view",
                            "payload": {
                                "content": "https://yandex.ru",
                                "need_authorization": true
                            }
                        }
                    }
                ]
            }
        }
    ]
}
```




### Бэкенд админки
Админка должна ходить в сервис `feeds-admin`, все пути к ручкам указаны относительно `feeds-admin.taxi.yandex.net`.

#### 1. Получить список сториз
```javascript
POST /v1/list
{
    "service": "eda-story",
    "skip": 0,
    "limit": 20,
    "filters": {
        "name": "то, что введено в строке поиска",

        // Если выбрано "Все кроме архивных"
        "status": ["created", "publishing", "published", "error"],

        // Если выбрано Архивные
        "status": ["finished"],

        // Если выбрано Опубликованные
        "status": ["publishing", "published", "error"]
    }
}
```

Ответ:
```javascript
{
    "service": "eda-story",
    "skip": 0,
    "limit": 20,
    "total": 100,
    "items": [{
        "id": "3f30427b198b4d56be1aecaf73c83597",
        "name": "story 1",
        // Остальные поля не используются
    }]
}
```


#### 2. Чтение конкретной сториз
```javascript
POST /v1/eda-promotions/get
{
    "id": "3f30427b198b4d56be1aecaf73c83597",
    "service": "eda-story"
}
```

Ответ:
```javascript
{
    "id": "3f30427b198b4d56be1aecaf73c83597",
    // Остальное как в ручке /create
}
```


#### 3. Создание сториз
```javascript
POST /v1/eda-promotions/create
{
    "name": "История Я.Еды",
    "service": "eda-story",

    "options": {
        "priority": 101,
        "screens": ["rest_list", "rest_menu"],
        "groups": ["carousel_1", "carousel_2"]
    },

    "payload": {
        // См. описание payload
    }
}
```

Ответ:
```javascript
{
    "id": "3f30427b198b4d56be1aecaf73c83597",
    "service": "eda-story",
    // Остальные поля не используются
}
```

#### 4. Сохранение сториз
```javascript
POST /v1/eda-promotions/update
{
    "id": "3f30427b198b4d56be1aecaf73c83597",
    "service": "eda-story",
    // Остальное как в /create
}
```

#### 5. Публикация сториз
```javascript
POST /v1/eda-promotions/publish
{
    "id": "3f30427b198b4d56be1aecaf73c83597",
    "service": "eda-story",
    "ticket": "TAXIINFRA-1",
    "experiment": "exp_name",
    "start_at": "2020-01-01T12:00:00Z",
    "finish_at": "2020-01-01T12:00:00Z"
}
```

#### 6. Снятие сториз с публикации
```javascript
POST /v1/eda-promotions/unpublish
{
    "id": "3f30427b198b4d56be1aecaf73c83597",
    "service": "eda-story"
}
```

#### 7. Архивация сториз
```javascript
POST /v1/eda-promotions/archive
{
    "id": "3f30427b198b4d56be1aecaf73c83597",
    "service": "eda-story"
}
```

#### 8. Загрузка медиа (на первом этапе только изображения)
Загрузка идемпотентна, ключ идемпотентности - хеш от content.
Ручка будет регистрировать медиа-объекты в `feeds` чтобы он знал как преобразовть `media_id` в URL медиа-обхекта. Для этого будет дергать ручку `<feeds>/v1/media/register`
```
POST /v1/media/upload
form-data:
   content: <binary>
```

Ответ:
```javascript
{
    "media_id": "3f30427b198b4d56be1aecaf73c83597"
}
```

#### 9. Чтение изображения
```
GET /v1/media/download?media_id=3f30427b198b4d56be1aecaf73c83597
```

Ответ: 
```
<binary jpg/png/...>
```

### База данных сообщений для продуктового API
API должно ходить в сервис `feeds`, все пути к ручкам указаны относительно `feeds.taxi.yandex.net`.

#### 1. Получение сториз
Когда пользователь приходит в продуктовое API, оно вычисляет под какие эксперименты он подпадает и подставляет имена экспериментов в запрос.

```javascript
POST /v1/fetch
{
    "service": "eda-story",

    // Локаль получателя.
    // Если какие-либо сториз не удается локализовать, то они не возвращаются
    "locale": "ru",

    // Параметры утсройства, которые влияют на размер медиа-объектов.
    // Надо указать либо screen_h+screen_w, либо size_hint+application.
    // Пример вычисления размера медиа: https://github.yandex-team.ru/taxi/rfc/blob/master/promotions/main.md
    "media_info": {
        "screen_height": 640,
        "screen_width": 960,

        "size_hint": 320,
        "application": "anrdoid"
    },
    
    "channels": [
        "user:<user_id>",
        "experiment:<exp1>",
        "experiment:<exp2>",
        // ...
        "experiment:<expN>"
    ]
}
```

Ответ:
```javascript
{
    // Список сториз
    "feed": [{
        "feed_id": "4fa4ea41013449edbce5429f3ac8f1b2",
        "created": "2019-01-21T23:00:01",
        "payload": {
            // См. описание payload.
            // Подставляются URL картинок вместо media_id, текст вместо ссылок на танкерные ключи
        },

        // Cтатус сториз.
        // Можно передавать в feeds статус "прочитано", "просмотрено" (через ручку /log_status).
        // Сначала может не использоваться.
        "last_status": {
            "status": "published",
            "created": "2019-01-21T23:00:01"
        },

        // API-сервис может хранить произвольные метаданные для каждого пользователя (через ручку /log_status).
        // Сначала может не использоваться.
        "meta": {}
    }],

    // Остальные поля не используются API
    "polling_delay": 300, // Рекомендуемый интервал опроса ручки /fetch
    "etag": "some-etag",  // Хеш-сумма переданных сообщений. Меняется если изменился набор сообщений или набор channels в запросе.
    "has_more": false     // Имеются ли еще сообщения для данного набора каналов. Для сториз всегда false.
}
```

#### 2. Запись статуса сториз для конкретного пользователя
Можно обновить статус прочтения сториз и записать произвольные метаданные в канале пользователя. Они вернутся в ответе ручки `/v1/fetch`.
Возможно, не потребуется на первом этапе.

```javascript
POST /v1/log_status
{
    "service": "eda-story",
    "feed_id": "4fa4ea41013449edbce5429f3ac8f1b2",
    "channel": "user:<user_id>",
    "status": "viewed" | "read",
    "meta": {
        "page_id": "news"
    }

}
```

#### 3. Удаление сториз у конкретного пользователя
Можно удалить сториз в канале пользователя - она больше не будет возвращаться `/v1/fetch`.
Возможно, не потребуется на первом этапе.

```javascript
POST /v1/remove
{
    "service": "eda-story",
    "feed_id": "4fa4ea41013449edbce5429f3ac8f1b2",
    "channel": "user:<user_id>"

}
```

#### 4. Регистрация медиа-объекта
Необходима чтобы `feeds` знал как преобразовывать `media_id` в URL.
Будет дергаться из `feeds-admin` при создании нового медиа-объекта.
```javascript
POST /v1/media/register
{
    "media_id": "4fa4ea41013449edbce5429f3ac8f1b2",
    "media_type": "image" | "video" | "animation"

    // Необходимо передать в feeds тип хранилища и путь к медиа в хранилище.
    // На первом этапе будут храниться только изображения в аватарнице.
    "storage": {
        "type": "avatars",
        "storage_media_id": "e5bb399de4e9493b9cec21f6430b4fec"
    }
}
```


### Список доработок инфраструктуры
Сервис `feeds-admin`
* Добавить `name` к рассылкам, научиться искать по нему (1д)
* Ручка `/v1/eda-promotions/get` (~1.5д)
* Ручка `/v1/eda-promotions/create` (~2д)
* Ручка `/v1/eda-promotions/update` (~1д)
* Ручка `/v1/eda-promotions/publish` (~2д)
* Ручка `/v1/eda-promotions/unpublish` (~1д)
* Ручка `/v1/eda-promotions/archive` (~0.5д)
* Ручка `/v1/media/upload` - поддержка только изображений через аватарницу (~5д)
* Ручка `/v1/media/download` (~2д)
* Помощь в тестировии, доработки (2д)
* Мелкие задачи: настройка АБК, графиков (2д)
* Риски (3д)

Итого: 23д

Сервис `feeds`
* Локализация (без оценки т.к. будет сделана для другого клиента)
* Ручка `/v1/media/register` (2д)
* Подстановка `media_id` (3д)
* Помощь в тестировании, доработки (2д)

Итого: 7д
