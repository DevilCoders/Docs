# Резолвер resolveStories

Возвращает сториз для приложения.

Данные в ответе резолвера нормализованы.

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `pageId` | number |  id cms-страницы типа app_stories с подборкой сторисов | - | - |
| `contentPreview`** | boolean | дебаг параметр для получения черновиков | - | false |
| `isLive` | boolean | Флаг, который регулирует выдачу, основываясь на актуальности трансляций. | true | |
| `isRanking` | boolean | Флаг персонализированной ленты сторисов. | false | |
| `experiment` | string | dj-эксперимент с данными | `market_app_live_stories` | - |
| `deviceId` | string | Идентификатор устройства | - | - |
| `idfa` | string | Рекламный идентификатор для iOS | - | - |
| `gaid` | string | Рекламный идентификатор для Android | - | - |

## Параметр `isLive`

Флаг, который регулирует выдачу, основываясь на актуальности трансляций.
Актуальная трансляция - это трансляция, имеющая статус "onair", или "scheduled" и времени до старта осталось меньше чем `actualBeforeStart`, или "finished" и времени с конца прошло меньше чем `actualAfterFinish`.
Если значение `isLive=true` и есть актуальные трансляции, то в ответ будут подмешаны сначала актуальные трансляции, а потом сторисы.
Если значение `isLive=true` и нет актуальных трансляций, то ответ будет пустым.
Если значение `isLive=false` и есть актуальные трансляции, то ответ будет пустым.
Если значение `isLive=false` и нет актуальных трансляций, то в ответе будет обычный набор сторисов.

## Пример ответа резолвера
```json
{
    "results": [
        {
            "handler": "resolveStories",
            "result": 107376
        }
    ],
    "collections": {
        "cmsPage": [
            {
                "id": 107376,
                "type": "app_stories",
                "hid": [
                    123,
                    333,
                    333
                ],
                "nid": [
                  777,
                  888
                ],
                "stories": [
                    {
                        "id": "nails_1",
                        "type": "onboarding",
                        "preview": {
                            "text": "Уход за ногтями",
                            "previewUrl": "https://white-market-mobile.s3.yandex.net/stories/nails/Nails_stories_preview_photoshadow@2x.jpg",
                            "previewColor": "ADE9FF"
                        },
                        "slides": [
                            {
                                "header": {
                                    "pictureUrl": "https://white-market-mobile.s3.yandex.net/stories/common/Avatar@3x.png",
                                    "title": "Яндекс.Маркет",
                                    "subTitle": "Полезные советы",
                                    "textColor": "FFFFFF"
                                },
                                "texts": {
                                    "title": "На Маркете тысячи средств для домашнего ухода за ногтями",
                                    "subTitle": "На Маркете тысячи средств для домашнего ухода за ногтями",
                                    "backgroundColor": "c69b78",
                                    "textColor": "FFFFFF"
                                },
                                "button": null,
                                "backgroundColor": "c69b78",
                                "pictureUrl": "https://white-market-mobile.s3.yandex.net/stories/nails/Nails_stories_1@2x.jpg",
                                "duration": 5000
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```

## Ссылки
- [Добавление и получение сториз](https://wiki.yandex-team.ru/market/ads/live/kak-sozdat-redaktorskuju-storis/)
