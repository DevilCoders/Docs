# Изменения в протоколе

Дизайн смотреть [здесь](https://www.figma.com/file/zWSt3vNWyrVQPQYX7YI23B/Go-%D0%9F%D0%BB%D1%8E%D1%81?node-id=26216%3A6206).
Для данного дизайна предлагается следующее описание.

- [Ручка v2](#ручка-v2)
  - [Новый тип айтемов - stories](#новый-тип-айтемов---stories)
  - [Текст справа от заголовка секции](#текст-справа-от-заголовка-секции)
  - [Новый тип айтемов - card](#новый-тип-айтемов---card)
  - [Подписи у секций](#подписи-у-секций)
- [Версионирование](#версионирование)
  - [Новый конфиг айтемов с идентификаторами](#новый-конфиг-айтемов-с-идентификаторами)
  - [Поддержка разных версий меню](#поддержка-разных-версий-меню)
- [Скоуп](#скоуп)

## Ручка v2

Для того, чтобы не выдумывать с внедрением в протокол существующей ручки, мы добавим v2 ручку `sdk-state`:

```
/4.0/sweet-home/v2/sdk-state
```

Протокол ручки будет повторять v1, но с некоторыми изменениями.

> В полном виде см. файл [full-menu.json5](./full-menu.json5) рядом.

### Новый тип айтемов - stories

Часть дизайна:

![](https://jing.yandex-team.ru/files/erakli00/stories.png)

Описание:

```json5
{
    "menu": {
        "sections": [
            {
                // добавляем тип секций. будем различать секции и разделители.
                "type": "section",

                // стиль оставляем, чтобы не делать множества изменений в АПИ
                "style": "default",
                "items": [
                    {
                        // добавляем тип айтемов - stories и list_item
                        "type": "stories",

                        // новое поле сторизов
                        "stories": {
                            // название экрана для АПИ communications
                            "screen_name": "house_of_plus:some_section",

                            // задаём параметры превью
                            "preview": {
                                // размер каждого превью в пикселях
                                "width": 322,
                                "height": 120
                            }
                        }
                    }
                ]
            },

            // нет сепаратора, пропускаю секцию "Как получить баллы"
    // ...
```

### Текст справа от заголовка секции

Часть дизайна:

![](https://jing.yandex-team.ru/files/erakli00/stories-with-list-item.png)

Описание:

```json5
    // ...
            {
                // дополнение протокола - может быть AttributedText или строка
                "title": "Как тратить баллы",

                "type": "section",
                "style": "default",

                // новое поле - стиль краёв секции
                "border_styles": {
                    "top": "default",    // default - край по-умолчанию (прямоугольный)
                    "bottom": "rounded"  // rounded - закруглённые углы
                },

                // новое поле - текст в правой части (обсуждаемо)
                "trail": {
                    "type": "default",

                    // AttributedText или строка
                    "title": "1 балл = 1 Р"
                },

                "items": [
                    {
                        "type": "stories",
                        "stories": {
                            "screen_name": "house_of_plus:another_section",
                            "preview": {
                                "width": 160,
                                "height": 240
                            }
                        }
                    },

                    // сразу после сторизов идёт лист айтем (Потратить на поездку)
                    {
                        // чтобы различать разные виды айтемов, используем 
                        // для существующих тип - list_item
                        "type": "list_item",

                        // переносим содержимое list_items в отдельное поле
                        "list_item": {
                            // остальное - как и раньше
                            "lead": {
                                "type": "default",
                                "title": "Потратить на поездку",
                                "subtitle": "Баланс: 70 баллов"
                            },
                            "trail": {
                                "type": "switch"
                            },
                            "action": {
                                "type": "SETTING",
                                "setting_id": "composite_payment.enabled"
                            }
                        }
                    }
                ]
            },

            {
                // добавляем специальный тип секций - разделитель
                "type": "separator"

                // BREAKING CHANGE - убираем обязательность поля items
            },
    // ...
```

### Новый тип айтемов - card


Часть дизайна:

![](https://jing.yandex-team.ru/files/erakli00/cards.png)

Описание:

```json5
    // ...
            // секция с кросс-сейлами
            {
                "type": "section",

                "style": "default",
                "border_styles": {
                    "top": "rounded",
                    "bottom": "rounded"
                },

                "items": [
                    {
                        // добавляем тип айтемов - card
                        "type": "card",

                        // новое поле карточек
                        "card": {
                            // AttributedText, цвет задаём через него
                            "title": {
                                "items": [
                                    {
                                        "type": "text",
                                        "text": "Кинопоиск HD",
                                        "font_size": 14,
                                        "font_weight": "bold",
                                        "color": "#000000"
                                    }
                                ]
                            },

                            // AttributedText
                            "subtitle": {
                                "items": [
                                    {
                                        "type": "text",
                                        "text": "В вашей подписке...",
                                        "font_size": 12,
                                        "font_weight": "regular",
                                        "color": "#000000"
                                    }
                                ]
                            },

                            // иконка перед заголовком
                            "icon": {
                                // как и в остальном протоколе иконка - объект типа Image
                                "url": "https://taxi-../bla-bla.png"
                            },
                            
                            // большая картинка на фоне
                            "background_image": {
                                "url": "https://taxi-../bla-bla.png"
                            },

                            // описание кнопки. будет зависеть от того, установленно ли приложение
                            "button": {
                                // AttributedText
                                "title": {
                                    "items": [
                                        {
                                            "type": "text",
                                            "text": "Смотреть",
                                            "font_size": 12,
                                            "font_weight": "regular",
                                            "color": "#000000"
                                        }
                                    ]
                                },

                                // объект Action, точно такой же, как и у ListItem
                                "action": {
                                    "type": "deeplink",
                                    "deeplink": "yandextaxi://<open kinopoisk app>"
                                },

                                "background_color": "#000000"
                            }
                        }
                    }
                ]
            },

            {
                "type": "separator"
            },
    // ...
```

Чтобы менять текст в зависимости от того, установлено ли соответствующее приложение на потребителе, в запросе к `/4.0/sweet-home/v2/sdk-state` клиенты должны передать список установленных приложений:

```json5
{
    "supported_features": [
        {
            "type": "app",
            "app": {
            
                // название приложения - music, kinopoisk
                "name": "kinopoisk",

                // установленно ли данное приложение на клиенте
                "installed": true  // true/false
            }
        }
    ]
}
```

### Подписи у секций

Часть дизайна:

![](https://jing.yandex-team.ru/files/erakli00/section-subtitle.png)

Описание:

```json5
    // ...
            {
                "type": "section",
                "title": "Кэшбэк баллами в кафе",

                // новое поле - подпись секции
                "subtitle": "При оплате счёта через Яндекс.Go вы получаете баллы на Плюс",

                "style": "default",
                "border_styles": {
                    "top": "rounded",
                    "bottom": "rounded"
                },

                "items": [
                    // QR-оплата, рестораны - здесь как и раньше, 
                    // но добавляем "type": "list_item"
                ]
            },
            {
                "type": "separator"
            },
            {
                "type": "section",

                "style": "default",
                "border_styles": {
                    "top": "rounded",
                    "bottom": "default"
                },

                "items": [
                    // подписка за баллы, вы в Плюсе - как и раньше,
                    // но добавляем "type": "list_item"
                ]
            }
        ]
    }
}
```

## Версионирование

Чтобы поддержать работу в двух версиях ручки, нужно уметь версионировать конфиги и модели.
Предлагается ввести следующие изменения:

- вынести элементы меню в отдельный конфиг с идентификаторами
- поддержать новые типы айтемов
- добавить поддержку разных версий меню в конфигах и моделях сервиса
- уметь переопределять порядок элементов

Это выливается в следующие изменения в конфигах.

### Новый конфиг айтемов с идентификаторами

Чтобы переиспользовать одни и те же айтемы в разных потребителях, предлагается добавить идентификаторы к айтемам в конфигах и моделях. 
Для этого добавляем конфиг `PLUS_SWEET_HOME_CLIENTS_UI_ITEMS`.
Пример конфига:

```json5
{
    // для удобства группируем элементы по сервису. в common будут лежать 
    // общие для всех сервисов элементы. в базе мы просто UNIQUE накинем потом
    "common": {

        // item_id - ключ мапы, для избежания дубликатов и визуального удобства
        "common:user_subscription": {

            // по типу будем парсить айтем
            "type": "list_item",
            "list_item": {

                // внутреннее наполнение не меняется

                "action": {
                    "need_authorization": true,
                    "type": "URL",
                    "url": "https://plus.yandex.ru"
                },
                "lead": {
                    "title_key": "sweet_home.menu.element.user_subscription.title"
                },
                "trail": {
                    "title_key": "sweet_home.menu.element.user_subscription.trail.title"
                }
            },
            "visibility_requirements": {
                "has_plus": true
            }
        },

        // новые типы айтемов также пойдут только в этот конфиг
        "common:card:kinopoisk:installed": {
            "type": "card",
            "card": {
                "title_key": "some_key",
                "subtitle_key": "some_key",
                "icon_tag": "icon_tag",
                "background_image_tag": "image_tag",
                "button": {
                    "title_key": "Смотреть",
                    "action": {
                        "type": "deeplink",
                        "deeplink": "yandextaxi://<open kinopoisk app>"
                    },
                    "background_color": "#000000"
                }
            },

            "visibility_requirements": {
            
                // какие приложения должны быть установлены/не установлены
                // на устройстве, чтобы данная карточка была видна
                "device_applications": {
                    "kinopoisk": {
                        "is_installed": true
                    }                
                }
            }
        },

        "common:card:kinopoisk:not_installed": {
            "type": "card",
            "card": {
                "title_key": "some_key",
                "subtitle_key": "some_key",
                "icon_tag": "icon_tag",
                "background_image_tag": "image_tag",
                "button": {
                    "title_key": "Установить",
                    "action": {
                        "type": "deeplink",
                        "deeplink": "yandextaxi://<install kinopoisk app>"
                    },
                    "background_color": "#000000"
                }
            },

            "visibility_requirements": {
            
                // какие приложения должны быть установлены/не установлены
                // на устройстве, чтобы данная карточка была видна
                "device_applications": {
                    "kinopoisk": {
                        "is_installed": false
                    }                
                }
            }
        },

        // в том числе и сторизы
        "common:stories:wide_promotions": {
            "type": "stories",
            "stories": {
                "screen_name": "house_of_plus:some_section",
                "preview": {
                    "width": 322,
                    "height": 120
                }
            }
        }
    },

    // пример группы для Такси
    "taxi": {
        "taxi:composite_payment": {
            "type": "list_item",
            "list_item": {
                "action": {
                    "setting_id": "composite_payment.enabled",
                    "type": "SETTING"
                },
                "lead": {
                    "subtitle_key": "sweet_home.settings.composite_payment.taxi.subtitle",
                    "title_key": "sweet_home.settings.composite_payment.taxi"
                }
            }
        },
        "taxi:qr_scanner": {
            "type": "list_item",
            "list_item": {
                "action": {
                    "deeplink": "yandextaxi://qr_scanner",
                    "type": "DEEPLINK"
                },
                "lead": {
                    "title_key": "sweet_home.menu.element.scan_qr_bill.title"
                },
                "trail": {
                    "icon_tag": "scan_qr_tag"
                }
            },
            "required_client_features": [
                "qr"
            ],
        }
    }
}
```

Возможные типы айтемов:

- `list_item`
- `stories`
- `card`

### Поддержка разных версий меню

Сейчас конфиг `PLUS_SWEET_HOME_CLIENTS_UI` выглядит следующим образом:

```json5
{
    // client_id
    "taxi.main": {
        "sdk_menu": {
            "sections": [
                // наполнение секций идёт сюда
            ]
        }
    }
}
```

Чтобы можно было переопределять наполнение меню в зависимости от подписочности пользователя и других признаков, будем задавать для каждого зарегистрированного клиента конфиг3.0 с описанием меню.
В конфиг `PLUS_SWEET_HOME_CLIENTS_UI` добавляем новое поле:

```json5
{
    // client_id
    "taxi.main": {
        // здесь мы оставляем секции для клиентов v1
        "sdk_menu": {
            "sections": [
                // наполнение старых секций идёт сюда
            ]
        },

        // описание v2 меню будет лежать в данном конфиге3.0
        "sdk_menu_v2_config30_name": "exp_name"
    }
}
```

В каждом конфиге3.0 будем задавать дефолтное состояние меню для конкретного потребителя.
Здесь мы поддержим идентификаторы и новые поля следующим образом (значение, которое возвращает конфиг3.0):

```json5
{
    // описание для дизайна выше
    "sections": [
        {
            "type": "section",
            "style": "default",
            "item_ids": [

                // используем идентификаторы из конфига PLUS_SWEET_HOME_CLIENTS_UI_ITEMS 

                "common:stories:wide_promotions"
            ]
        },
        {
            "type": "section",
            "style": "default",

            // в v2 задаём стили краёв секции
            "border_styles": {
                "top": "default",    // default - край по-умолчанию (прямоугольный)
                "bottom": "rounded"  // rounded - закруглённые углы
            },

            "title_key": "Как тратить баллы",

            // здесь переиспользуем ItemElement из v1
            "trail": {
                "type": "default",
                "title_key": "1 балл = 1 Р"
            },

            "item_ids": [
                "common:stories:spend_points",
                "taxi:composite_payment"
            ]
        },
        {
            "type": "separator"
        },
        {
            "type": "section",
            "style": "default",
            "border_styles": {
                "top": "rounded",
                "bottom": "rounded"
            },
            "item_ids": [
                "common:card:kinopoisk",
                "common:card:music",
            ]
        }

        // и тд
    ],
}
```

В отдельных клозах будем задавать переопределяющее состояние.
С помощью кодогенерации, мы будем пользоваться конфигом3.0 абсолютно также, как и обычными конфигами.
При этом, все состояния для конкретного потребителя будут храниться в одном месте.

## Скоуп

> Высчитанные по особой методике "palcem v nebo" сроки задач также прилагаются.

- затащить кэш картинок (согласования + интерфейсы) - 3 дня
- затащить использование библиотеки extended-template для AttributedText (внедриться в Translator) - 3 дня
- поддержать типы в секциях (+ v2 презентеры) - 1 день
- поддержать карточки кросс-сейла (+ v2 презентеры) - 2 дня
- поддержать секцию сторизов (+ v2 презентеры) - 1-2 дня
- версионирование UI для ручки sdk-state (скорее на подумать, но возможно придётся с конфигами выдумывать) - 1-3 дней
- v2 ручка (контекст + тесты) - 2-3 дня
