# Хендлер resolveFlatCms
Ходит за определенной страницей в cms, которая возвращает список виджетов, которые содержат ресурсы, которыми надо заполнить виджет.
Ресурс бывает статический и динамический. Статические ресурсы отдаем как есть. Динамический ресурс - это хендлер
с параметрами, который надо вызвать. Таких хендлеров может быть много. Вызываем все за раз, прогоняем их через ассемблеры -
функции, преобразующие ответ в нужный формат, растаскиваем ресурсы назад к виджетам.
В итоге получаем сразу наполненную всеми данными страницу, например главную, для мобилки.
Разработано в рамках тикета [MARKETFRONT-65641](https://st.yandex-team.ru/MARKETFRONT-65641)

<br>Зачем так, a не просто вызвать хендлеры:
<br>Хендлеры отдают избыточный ответ, который тяжело парсить на мобилках. Здесь после похода в хендлер  к нему
применяется "ассемблер" - функция, которая из result и collections собирает компактный ответ
<br> С клиента приходит всего один запрос, все остальные идут с ФАПИ в ФАПИ

## Параметры

```
type FlatCmsParams ={
            "cmsParams":{
               "type": string,
               "target": {
                   "type": string,
                   "getAllWidgets": boolean,
                   "pageToken": sring|null,
                   "loadWidgetsPage": boolean,
                   "widgetIds": Array<number>
               }
            },
            "resolversParams": any
        }
```

###FlatCmsParams.cmsParams

| Parameter                | Type    | Description                                     | Default | Value |
|--------------------------|---------|-------------------------------------------------|------------------| ------- |
| `type`*                  | string  | какую страницу запросить                        | - | - |
| `target.getAllWidgets`   | boolean | отдать все виджеты без пагинации                | - | - |
| `target.type`*           | string  | тип ответа, который хотим: document или widgets | - | - |
| `target.widgetIds`       | Array<number> | отдать конкретные виджеты                       | - | - |
| `target.loadWidgetsPage`* | boolean | тип ответа, который хотим: document или widgets | - | - |


###FlatCmsParams.resolversParams

| Parameter | Type | Description                                                    | Default | Value |
|-----------|------|----------------------------------------------------------------|------------------| ------- |
| [string]  | any  | любые параметры для резолверов, которыми надо заменить шаблоны | - | - |


\* - обязательные параметры

## Пример запроса
```bash
curl --location --request POST 'https://ipa.market.yandex.ru/api/v1?gps=37.49453011558516%2C55.77339823403054&name=resolveFlatCms&dictionary=true&rearr-factors=test-resources' \
--header 'Accept: application/json,text/plain' \
--header 'Content-Type: application/json' \
--data-raw '{
  "params": [
    {
      "cmsParams": {
        "type": "apps_home_page",
        "target": {
          "type": "document",
          "getAllWidgets": true,
          "pageToken": null,
          "loadWidgetsPage": true,
          "widgetIds": []
        }
      },
      "resolversParams": {}
    }
  ]
}'
```
#Пример ответа
```json
{
    "results": [
        {
            "handler": "resolveFlatCms",
            "result": {
                "document": {
                    "id": 193755,
                    "type": "apps_home_page",
                    "meta": {
                        "documentType": "apps_home_page",
                        "documentName": "Главная",
                        "documentId": 193755,
                        "revisionId": 4458317,
                        "schemaCommit": "15718e60bbe1b459dece73fee2bb6378dfb81b8b",
                        "updatedTimestamp": "2022-01-26T14:19:05Z"
                    },
                    "domain": {
                        "entity": "binding",
                        "domain": "ru"
                    },
                    "bindings": [],
                    "entity": "document",
                    "djParams": "experiment=get_context_blender",
                    "recom_context": "eJzjYuKQ5GLi0Odi5vjGBCRugIh1zEAhNSDjLQuQ2A0izrABhfSAmBOI2YEC0xmBxCxGIM8ViOuBnJsgra9BwhPYgMRskBwXEFsDsRBQoBckOgMkqgkAdvIOZA,,",
                    "widgetSet": "default"
                },
                "widgets": [
                    {
                        "hotlinks": {
                            "hotlinks": [
                                {
                                    "type": "deeplink",
                                    "deeplink": "yamarket://browser?hybrid-mode=1&url=https%3A%2F%2Fm.market.yandex.ru%2Fspecial%2Fnew-year2022",
                                    "title": "Новый год",
                                    "imageUrl": "//avatars.mds.yandex.net/get-marketcms/1534436/img-33ff9e97-698e-4e4e-8702-e21277d0a057.png/optimize"
                                },
                                {
                                    "type": "deeplink",
                                    "deeplink": "yamarket://catalog/54440",
                                    "title": "Электроника",
                                    "imageUrl": "//avatars.mds.yandex.net/get-marketcms/879900/img-bb3cddaf-b1c0-4785-b9a1-cf542ae07c95.png/optimize"
                                },
                                {
                                    "type": "deeplink",
                                    "deeplink": "yamarket://catalog/54419",
                                    "title": "Бытовая техника",
                                    "imageUrl": "//avatars.mds.yandex.net/get-marketcms/879900/img-41d8e38a-4f7a-47cd-ab03-aa49421a2be1.png/optimize"
                                }
                            ],
                            "id": 111818695,
                            "type": "static",
                            "entity": "resource"
                        },
                        "autoplay": true,
                        "looped": true,
                        "id": 111818683,
                        "type": "BannersCarouselWithHotlinksWidget",
                        "reloadable": false,
                        "entity": "widget",
                        "content": [],
                        "errors": [
                            {
                                "kind": "assembler error",
                                "message": "Resource with id 111818684 has no assembler"
                            }
                        ]
                    },
                    {
                        "title": "Акции",
                        "minCountToShow": null,
                        "id": 111818858,
                        "type": "PromoLandingsScrollboxWidget",
                        "reloadable": false,
                        "entity": "widget",
                        "content": [
                            {
                                "id": "6495a2a3d7273d05320f8bd016c88258",
                                "title": "Акции и скидки",
                                "subtitle": "На всё, чем стоит запастись",
                                "endDate": "2021-01-31",
                                "pictureUrl": "//avatars.mds.yandex.net/get-marketcms/944743/img-4c80124c-754f-45a1-95ed-3483b4e8dc4b.jpeg/optimize",
                                "url": "https://pokupki.market.yandex.ru/special/EVERY-DAY"
                            },
                            {
                                "id": "b017e71b20feca6c4b729b49acedd233",
                                "title": "Товары для хобби и творчества",
                                "endDate": "2022-01-31",
                                "pictureUrl": "//avatars.mds.yandex.net/get-marketcms/1533751/img-54b2c511-2cb2-431f-bb5c-c4231060419f.jpeg/optimize",
                                "url": "https://market.yandex.ru/special/januaryholidayprr"
                            }
                        ],
                        "errors": []
                    },
                    {
                        "id": 111818941,
                        "type": "BannerWidget",
                        "reloadable": false,
                        "entity": "widget",
                        "content": [],
                        "errors": [
                            {
                                "kind": "HandlerOfResolveFenekBannersError",
                                "message": "Param \"banners\" is not an array ([object Object])"
                            }
                        ]
                    },
                    {
                        "title": "Мои недавние находки",
                        "minCountToShow": 3,
                        "showMore": null,
                        "snippet": {
                            "withTitle": false,
                            "withPrice": true,
                            "withRating": false,
                            "withCashback": false,
                            "withPromocode": false,
                            "withProducingCountry": false,
                            "withReasonsToBuy": false,
                            "withCartButton": true,
                            "hideTimer": false,
                            "showWishlistToggler": false
                        },
                        "timer": null,
                        "id": 111818962,
                        "type": "ProductScrollboxWidget",
                        "reloadable": false,
                        "entity": "widget",
                        "content": [],
                        "errors": []
                    },
                    {
                        "title": "Может заинтересовать",
                        "id": 111818968,
                        "type": "ProductsRollWidget",
                        "reloadable": false,
                        "entity": "widget",
                        "content": [

                            {
                                "title": "Наушники Sony WH-1000XM3 Black",
                                "pictures": [
                                    "https://avatars.mds.yandex.net/get-marketpic/1604894/pic6c2743c812acf4bb538a06d1d486545c/orig"
                                ],
                                "price": {
                                    "value": 16490,
                                    "sign": "₽"
                                },
                                "rating": 4.63,
                                "opinionsCount": 414
                            },
                            {
                                "title": "Наклейки на самоклеящейся пленке, серебряные, d 70 мм - 100 шт",
                                "pictures": [
                                    "https://avatars.mds.yandex.net/get-mpic/5207439/img_id8151066291504538301.jpeg/orig"
                                ],
                                "price": {
                                    "value": 550,
                                    "sign": "₽"
                                },
                                "rating": 0,
                                "opinionsCount": 0
                            }
                        ],
                        "errors": []
                    }
                ],
                "pageToken": "0"
            }
        }
    ],
    "collections": {}
}
```
