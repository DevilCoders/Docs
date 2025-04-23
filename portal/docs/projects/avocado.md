## Avocado API

Бэкенд Авокадо в виде Go-серванта живет в отдельном [Nanny-сервисе](https://nanny.yandex-team.ru/ui/#/services/catalog/avocado/)

YP-эндпоинт сеты:
* Продакшн: avocado
* Тестинг: avocado-testing

В Хорайзоне бэкенд Авокадо называется [MORDA__AVOCADO_SERVICE](https://horizon.z.yandex-team.ru/backends?arcpath=trunk&textFilter=MORDA__AVOCADO_SERVICE)

Обращаться к нему стоит через геохелпер либо авохамстер, которые понимают запрос, описанный ниже.

### `POST /geohelper_avocado/top_news`
Формирует div-ную карточку с данными наиболее популярных новостей.

Входные данные: JSON со следующими полями:
* `url: string` – URL запроса в ручку Новостей, по которому будут забираться данные
для формирования. Используются только CGI-параметры (часть после `?`), хост и путь игнорируются.
* `scale_factor: float64` - коэффициент масштаба для рендера, должен быть положительным числом с плавающей точкой.
* `ordered_rubrics: string[]` –  список рубрик, в порядке которого будут отображаться табы Новостей.
* `locale: string` – локаль поискового приложения, на язык которой будут переводиться названия табов и других элементов карточки.


Выходные данные: JSON с div-вёрсткой карточки в том формате, в каком её отдаёт Geohelper.

Пример запроса:

```json
{
    "url": "https://news.stable.priemka.yandex.ru/api/v2/tops_export?client=morda&doclang=ru&issue=ru&preset=morda_export_touch&stories_count=1",
    "scale_factor": 1.5,
    "ordered_rubrics": [
        "index",
        "business",
        "politics"
    ],
    "locale": "ru"
}
```
{% cut "Пример ответа" %}
```json
{
    "div_templates": {
        "commonCardHeader": {
            "type": "container",
            "items": [
                {
                    "type": "text",
                    "paddings": {
                        "left": 16,
                        "top": 12,
                        "bottom": 12
                    },
                    "action": {
                        "log_id": "title",
                        "$url": "cardUrl"
                    },
                    "font_size": 18,
                    "font_weight": "medium",
                    "line_height": 20,
                    "text_color": "#cc000000",
                    "$text": "title"
                },
                {
                    "type": "image",
                    "height": {
                        "type": "fixed",
                        "value": 44,
                        "unit": "sp"
                    },
                    "width": {
                        "type": "fixed",
                        "value": 44,
                        "unit": "sp"
                    },
                    "action": {
                        "log_id": "menu",
                        "menu_items": [
                            {
                                "action": {
                                    "log_id": "menu/item/0",
                                    "url": "opensettings://?screen=feed"
                                },
                                "$text": "settingsText"
                            },
                            {
                                "action": {
                                    "log_id": "menu/item/1",
                                    "$url": "hideCardUrl"
                                },
                                "$text": "hideCardText"
                            }
                        ]
                    },
                    "image_url": "https://yastatic.net/s3/home/yandex-app/services_div/general/menu_points.3.png",
                    "placeholder_color": "#00ffffff"
                }
            ],
            "orientation": "horizontal"
        },
        "ghRedesignBlockIcon/bd6ff34a9f7be23d92f61bbc6d3d4631": {
            "type": "image",
            "margins": {
                "right": 8
            },
            "border": {
                "corner_radius": 18
            },
            "height": {
                "type": "fixed",
                "value": 36
            },
            "width": {
                "type": "fixed",
                "value": 36
            },
            "$image_url": "icon"
        },
        "ghRedesignBlockTitleSimple/d8cdb92094ee0183b398778b20bceb59": {
            "type": "text",
            "font_size": 16,
            "font_weight": "medium",
            "line_height": 20,
            "$text": "title"
        },
        "ghRedesignBlockMenu/d04ed6e49aedf8f22ff4782c04c339ce": {
            "type": "image",
            "height": {
                "type": "fixed",
                "value": 36,
                "unit": "sp"
            },
            "width": {
                "type": "fixed",
                "value": 36,
                "unit": "sp"
            },
            "alignment_horizontal": "right",
            "action": {
                "log_id": "menu",
                "menu_items": [
                    {
                        "action": {
                            "log_id": "menu/item/0",
                            "url": "opensettings://?screen=feed"
                        },
                        "$text": "settingsText"
                    },
                    {
                        "action": {
                            "log_id": "menu/item/1",
                            "$url": "hideCardUrl"
                        },
                        "$text": "hideCardText"
                    }
                ]
            },
            "placeholder_color": "#00ffffff",
            "$image_url": "menuPoints"
        },
        "ghRedesignBlockHead3/0ecd8eeee190bf0d5c3a20bf63fad52a": {
            "type": "container",
            "margins": {
                "bottom": 10,
                "top": 10,
                "left": 16,
                "right": 14
            },
            "content_alignment_vertical": "center",
            "orientation": "horizontal"
        },
        "newsTopTab/dfeac164fed558bae953e0afe00b3b36": {
            "type": "container",
            "height": {
                "type": "match_parent"
            },
            "items": [
                {
                    "type": "container",
                    "paddings": {
                        "top": 5,
                        "bottom": 5
                    },
                    "margins": {
                        "left": 4,
                        "right": 4
                    },
                    "border": {
                        "corner_radius": 20
                    },
                    "height": {
                        "type": "match_parent"
                    },
                    "background": [
                        {
                            "type": "solid",
                            "color": "#F1F2F6"
                        }
                    ],
                    "$items": "stories"
                },
                {
                    "type": "text",
                    "margins": {
                        "bottom": 16,
                        "left": 20,
                        "top": 16
                    },
                    "font_size": 14,
                    "font_weight": "medium",
                    "line_height": 16,
                    "$text": "footerText",
                    "$action": "footerAction"
                }
            ]
        },
        "newsTopItemIcon/0fe33af0945e25eaf3fe4378d2aed628": {
            "type": "image",
            "border": {
                "corner_radius": 3
            },
            "height": {
                "type": "fixed",
                "value": 16
            },
            "width": {
                "type": "fixed",
                "value": 16
            },
            "scale": "fit",
            "$image_url": "iconUrl"
        },
        "newsTopTabItem/c3521277d5e28f33a4add0afac34c85e": {
            "type": "container",
            "items": [
                {
                    "type": "container",
                    "margins": {
                        "left": 12,
                        "right": 12,
                        "top": 9,
                        "bottom": 9
                    },
                    "items": [
                        {
                            "type": "container",
                            "paddings": {
                                "top": 2,
                                "left": 4
                            },
                            "height": {
                                "type": "fixed",
                                "value": 22
                            },
                            "width": {
                                "type": "fixed",
                                "value": 32
                            },
                            "alignment_horizontal": "center",
                            "alignment_vertical": "top",
                            "orientation": "overlap",
                            "$items": "icon"
                        },
                        {
                            "type": "text",
                            "font_size": 16,
                            "line_height": 20,
                            "max_lines": 3,
                            "$text": "title"
                        }
                    ],
                    "content_alignment_vertical": "center",
                    "orientation": "horizontal"
                }
            ]
        },
        "ghRedesignTabs/4c5e967a77012e995bc7456c96da966f": {
            "type": "tabs",
            "tab_title_style": {
                "active_text_color": "#CC000000",
                "inactive_text_color": "#CC000000",
                "font_weight": "medium",
                "font_size": 14,
                "line_height": 18
            },
            "title_paddings": {
                "left": 14,
                "right": 14,
                "bottom": 8
            },
            "$items": "tabs"
        },
        "ghRedesignBlock/679d4ef2679e48917f7e40949f9990f4": {
            "type": "container",
            "border": {
                "corner_radius": 24
            },
            "background": [
                {
                    "type": "solid",
                    "color": "#FFF"
                }
            ]
        }
    },
    "ttv": 1200,
    "ttl": 300,
    "country": "RU",
    "api_version": "2",
    "utime": 1626809906,
    "geo_country": 0,
    "layout": [],
    "msid": "2117365356.299.1626809906440.61739",
    "api_name": "search",
    "geo": 213,
    "block": [
        {
            "id": "topnews",
            "type": "div2",
            "topic": "topnews_card",
            "utime": 1626809906,
            "data": {
                "log_id": "topnews",
                "states": [
                    {
                        "state_id": 1,
                        "div": {
                            "type": "ghRedesignBlock/679d4ef2679e48917f7e40949f9990f4",
                            "items": [
                                {
                                    "type": "ghRedesignBlockHead3/0ecd8eeee190bf0d5c3a20bf63fad52a",
                                    "items": [
                                        {
                                            "type": "ghRedesignBlockIcon/bd6ff34a9f7be23d92f61bbc6d3d4631",
                                            "icon": "https://yastatic.net/s3/home/div/icons/topnews_div2.1.5.png",
                                            "action": {
                                                "url": "https://yandex.ru/news",
                                                "log_id": "base_tabbed_card_icon"
                                            }
                                        },
                                        {
                                            "type": "ghRedesignBlockTitleSimple/d8cdb92094ee0183b398778b20bceb59",
                                            "title": "Сейчас в СМИ",
                                            "action": {
                                                "url": "https://yandex.ru/news",
                                                "log_id": "card title"
                                            }
                                        },
                                        {
                                            "type": "ghRedesignBlockMenu/d04ed6e49aedf8f22ff4782c04c339ce",
                                            "menuPoints": "https://yastatic.net/s3/home/yandex-app/services_div/redesign/zen_menu_dark.3.png",
                                            "hideCardText": "Скрыть карточку",
                                            "settingsText": "Настройки ленты",
                                            "hideCardUrl": "hidecard://?topic_card_ids=topnews_card&undo_snackbar_text=%D0%92%D1%8B%20%D1%81%D0%BA%D1%80%D1%8B%D0%BB%D0%B8%20%D0%BA%D0%B0%D1%80%D1%82%D0%BE%D1%87%D0%BA%D1%83"
                                        }
                                    ]
                                },
                                {
                                    "type": "ghRedesignTabs/4c5e967a77012e995bc7456c96da966f",
                                    "dynamic_height": 1,
                                    "tabs": [
                                        {
                                            "title": "Главное",
                                            "title_click_action": {
                                                "log_id": "tab title/click/0",
                                                "url": "https://yandex.ru/news"
                                            },
                                            "div": {
                                                "type": "newsTopTab/dfeac164fed558bae953e0afe00b3b36",
                                                "stories": [
                                                    {
                                                        "type": "newsTopTabItem/c3521277d5e28f33a4add0afac34c85e",
                                                        "icon": [
                                                            {
                                                                "type": "newsTopItemIcon/0fe33af0945e25eaf3fe4378d2aed628",
                                                                "iconUrl": "https://avatars.mds.yandex.net/get-ynews-logo/135513/1002-1544074003449-square/logo"
                                                            }
                                                        ],
                                                        "title": "Первый полет нового военного российского истребителя запланировали на 2023 год",
                                                        "action": {
                                                            "url": "yellowskin://?url=https%3A%2F%2Fyandex.ru%2Fnews%2Fstory%2FPervyj_polet_novogo_voennogo_rossijskogo_istrebitelya_zaplanirovali_na2023_god--6bb4d3282b0d2be08f1652737d5d53aa%3Flang%3Dru%26from%3Dmain_portal%26wan%3D1%26stid%3DbFee5GL5vNRANww5VzcU%26t%3D1626809440%26persistent_id%3D153654178%26wan%3D1%26utm_medium%3Dtopnews_index%26utm_source%3Dmorda_pp",
                                                            "log_id": "tabs/0/item 0"
                                                        }
                                                    }
                                                ],
                                                "footerText": "Все новости",
                                                "footerAction": {
                                                    "log_id": "tabs/0/full list",
                                                    "url": "https://yandex.ru/news"
                                                }
                                            }
                                        },
                                        {
                                            "title": "Россия",
                                            "title_click_action": {
                                                "log_id": "tab title/click/1",
                                                "url": "https://yandex.ru/news/region/Russia"
                                            },
                                            "div": {
                                                "type": "newsTopTab/dfeac164fed558bae953e0afe00b3b36",
                                                "stories": [
                                                    {
                                                        "type": "newsTopTabItem/c3521277d5e28f33a4add0afac34c85e",
                                                        "icon": [
                                                            {
                                                                "type": "newsTopItemIcon/0fe33af0945e25eaf3fe4378d2aed628",
                                                                "iconUrl": "https://avatars.mds.yandex.net/get-ynews-logo/786982/254102416-1554223959149-square/logo"
                                                            }
                                                        ],
                                                        "title": "Начальник УГИБДД задержан на Ставрополье по подозрению во взятках",
                                                        "action": {
                                                            "url": "yellowskin://?url=https%3A%2F%2Fyandex.ru%2Fnews%2Fstory%2FNachalnik_UGIBDD_zaderzhan_naStavropole_popodozreniyu_vo_vzyatkakh--7cf5f10244bd1b7eafbd4d7f3f6c4b4e%3Flang%3Dru%26from%3Dreg_portal%26wan%3D1%26stid%3DMrE5qGW6bhiTDyz8BVKT%26t%3D1626809440%26persistent_id%3D153649411%26utm_medium%3Dtopnews_Russia%26utm_source%3Dmorda_pp",
                                                            "log_id": "tabs/1/item 0"
                                                        }
                                                    }
                                                ],
                                                "footerText": "Все новости региона",
                                                "footerAction": {
                                                    "log_id": "tabs/1/full list",
                                                    "url": "https://yandex.ru/news/region/Russia"
                                                }
                                            }
                                        },
                                        {
                                            "title": "Экономика",
                                            "title_click_action": {
                                                "log_id": "tab title/click/2",
                                                "url": "https://yandex.ru/news/rubric/business"
                                            },
                                            "div": {
                                                "type": "newsTopTab/dfeac164fed558bae953e0afe00b3b36",
                                                "stories": [
                                                    {
                                                        "type": "newsTopTabItem/c3521277d5e28f33a4add0afac34c85e",
                                                        "icon": [
                                                            {
                                                                "type": "newsTopItemIcon/0fe33af0945e25eaf3fe4378d2aed628",
                                                                "iconUrl": "https://avatars.mds.yandex.net/get-ynews-logo/135513/1002-1544074003449-square/logo"
                                                            }
                                                        ],
                                                        "title": "Более 200 миллиардов рублей выделят на авиастроение в России на 3 года",
                                                        "action": {
                                                            "url": "yellowskin://?url=https%3A%2F%2Fyandex.ru%2Fnews%2Fstory%2FBolee_200_milliardov_rublej_vydelyat_naaviastroenie_vRossii_na3_goda--d20bfe75db4dc3a990a429df2f55dfaa%3Flang%3Dru%26from%3Drub_portal%26wan%3D1%26stid%3DxixiTC6uWcMTU_-5jiQS%26t%3D1626809440%26persistent_id%3D153678331%26utm_medium%3Dtopnews_business%26utm_source%3Dmorda_pp",
                                                            "log_id": "tabs/2/item 0"
                                                        }
                                                    }
                                                ],
                                                "footerText": "Все новости экономики",
                                                "footerAction": {
                                                    "log_id": "tabs/2/full list",
                                                    "url": "https://yandex.ru/news/rubric/business"
                                                }
                                            }
                                        },
                                        {
                                            "title": "Политика",
                                            "title_click_action": {
                                                "log_id": "tab title/click/3",
                                                "url": "https://yandex.ru/news/rubric/politics"
                                            },
                                            "div": {
                                                "type": "newsTopTab/dfeac164fed558bae953e0afe00b3b36",
                                                "stories": [
                                                    {
                                                        "type": "newsTopTabItem/c3521277d5e28f33a4add0afac34c85e",
                                                        "icon": [
                                                            {
                                                                "type": "newsTopItemIcon/0fe33af0945e25eaf3fe4378d2aed628",
                                                                "iconUrl": "https://avatars.mds.yandex.net/get-ynews-logo/135513/1002-1544074003449-square/logo"
                                                            }
                                                        ],
                                                        "title": "Первый полет нового военного российского истребителя запланировали на 2023 год",
                                                        "action": {
                                                            "url": "yellowskin://?url=https%3A%2F%2Fyandex.ru%2Fnews%2Fstory%2FPervyj_polet_novogo_voennogo_rossijskogo_istrebitelya_zaplanirovali_na2023_god--6bb4d3282b0d2be08f1652737d5d53aa%3Flang%3Dru%26from%3Drub_portal%26wan%3D1%26stid%3DbFee5GL5vNRANww5VzcU%26t%3D1626809440%26persistent_id%3D153654178%26utm_medium%3Dtopnews_politics%26utm_source%3Dmorda_pp",
                                                            "log_id": "tabs/3/item 0"
                                                        }
                                                    }
                                                ],
                                                "footerText": "Все новости политики",
                                                "footerAction": {
                                                    "log_id": "tabs/3/full list",
                                                    "url": "https://yandex.ru/news/rubric/politics"
                                                }
                                            }
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ]
            },
            "heavy": 1
        }
    ],
    "lang": "ru"
}
```
{% endcut %}

## Cоздание http запроса в IDE
Данная инструкция распространяется на IDE от JetBrains.
* Создаем http файл: **File - New - HTTP Request** (созданные *.http файлы нужно добавить в arcignore в папке portal, чтобы они не попали в транк).
* Пример запроса:
```json
POST http://avocado-dev.yandex.net/geohelper_avocado/top_news?srcrwr=MORDA__AVOCADO_SERVICE:morda-dev-vXXX.sas.yp-c.yandex.net:<port>
Accept: application/json
content-type: application/json

{
    "url": "https://news.stable.priemka.yandex.ru/api/v2/tops_export?client=morda&doclang=ru&issue=ru&preset=morda_export_touch&stories_count=1",
    "scale_factor": 1.5,
    "ordered_rubrics": [
        "index",
        "business",
        "politics"
    ],
    "locale": "ru"
}
```
* Далее делаем **Run all requests in file - Run with no environment**
* Для дебага можете добавить отладочные параметры в ваш запрос: https://docs.yandex-team.ru/apphost/pages/cgi
* Также для дебага будет полезно посмотреть [SeTrace](https://setrace.yandex-team.ru/web/search). ID вашего запроса можно найти в заголовке **X-Yandex-Req-Id**.

