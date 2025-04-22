# Резолвер resolveStoriesByIds

Возвращает сториз для приложения по айдишникам

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `pageIds` | number[] |  id cms-страницы типа app_stories с подборкой сторисов | - | - |
| `contentPreview`** | boolean | дебаг параметр для получения черновиков | - | false |

## Пример ответа резолвера
```json
{
    "results": [
        {
            "handler": "resolveStoriesByIds",
            "result": [157056, 161242]
        }
    ],
    "collections": {
        "cmsPage": {
           "157056": {
                "id": 157056,
                "type": "app_story",
                "bindings": [
                    {
                        "entity": "sku",
                        "id": "101385201094"
                    }
                ],
                "stories": {
                    "id": "live_157056",
                    "pageId": 157056,
                    "preview": {
                        "text": "Этих раскрасок вам хватит надолго",
                        "previewUrl": "//avatars.mds.yandex.net/get-marketcms/1534436/img-57aaf980-0d09-4920-99fa-4501e6c9ec64.jpeg/optimize",
                        "previewColor": null,
                        "textColor": "FFFFFF",
                        "shading": true
                    },
                    "slides": [
                        {
                            "header": {
                                "pictureUrl": "//avatars.mds.yandex.net/get-marketcms/0/img-0.png/optimize",
                                "title": null,
                                "subTitle": null,
                                "textColor": null,
                                "closeButtonColor": "AAFFFFFF"
                            },
                            "texts": null,
                            "button": null,
                            "backgroundColor": "000000",
                            "pictureUrl": null,
                            "videoContentId": "495448f90618bb1fb1c1b0d3082b38e0",
                            "duration": 52000
                        }
                    ],
                    "analytics": null,
                    "skuConfig": {
                        "params": {
                            "sku": [
                                101385201094
                            ],
                            "shop-promo-id": null,
                            "hideOffersWithNoGifts": null,
                            "filter-discount-only": null,
                            "warehouse_id": null,
                            "supplier-id": [],
                            "use-default-offers": "1",
                            "hideMskuWithoutOffers": null
                        },
                        "id": "RootSkuByIds"
                    },
                    "dateStart": null,
                    "dateEnd": null,
                    "sponsored": null,
                    "skuIds": [
                        "101385201094"
                    ]
                }
            },
           "161242": {
                "id": 161242,
                "type": "app_story",
                "bindings": [
                    {
                        "entity": "sku",
                        "id": "101232764790"
                    }
                ],
                "stories": {
                    "id": "live_161242",
                    "pageId": 161242,
                    "preview": {
                        "text": "Аккумуляторный шуруповёрт Elitech",
                        "previewUrl": "//avatars.mds.yandex.net/get-marketcms/1779479/img-2ee99300-2839-4337-84a6-d53ed6705331.jpeg/optimize",
                        "previewColor": null,
                        "textColor": "FFFFFF",
                        "shading": true
                    },
                    "slides": [
                        {
                            "header": {
                                "pictureUrl": "//avatars.mds.yandex.net/get-marketcms/0/img-0.png/optimize",
                                "title": null,
                                "subTitle": null,
                                "textColor": null,
                                "closeButtonColor": "AAFFFFFF"
                            },
                            "texts": null,
                            "button": null,
                            "backgroundColor": "000000",
                            "pictureUrl": null,
                            "videoContentId": "4b9a3cb84b802607a00451f5b04552e1",
                            "duration": 58000
                        }
                    ],
                    "analytics": null,
                    "skuConfig": {
                        "params": {
                            "sku": [
                                101232764790
                            ],
                            "shop-promo-id": null,
                            "hideOffersWithNoGifts": null,
                            "filter-discount-only": null,
                            "warehouse_id": null,
                            "supplier-id": [],
                            "use-default-offers": "1",
                            "hideMskuWithoutOffers": null
                        },
                        "id": "RootSkuByIds"
                    },
                    "dateStart": null,
                    "dateEnd": null,
                    "sponsored": null,
                    "skuIds": [
                        "101232764790"
                    ]
                }
            }
        }
    }
}
```

## Ссылки
- [Добавление и получение сториз](https://wiki.yandex-team.ru/market/ads/live/kak-sozdat-redaktorskuju-storis/)
