# Хендлер resolveCmsResource
Получает на вход параметры для хендлера, который надо вызвать и ходит в него через внутренний балансер
<br>Зачем так, a не просто вызвать хендлер:
<br>Хендлеры отдают избыточный ответ, который тяжело парсить на мобилках. Здесь после похода в хендлер  к нему
применяется "ассемблер" - функция, которая из result и collections собирает компактный ответ <br>
Разработано в рамках тикета [MARKETFRONT-65641](https://st.yandex-team.ru/MARKETFRONT-65641)

## Параметры

```
type CmsResourceParams =  {
   "resolvers":[
      {
         "resolver"*:"string", // имя хендлера
         "version"*:"string", // версия
         "params"*:"any" // параметры для хендлера
      }
   ],
   "assembler"*:{
      "type"*:"string" // каким образом собрать ответ
   }
}
```

| Parameter         | Type              | Description                                                 | Default | Value |
|-------------------|-------------------|-------------------------------------------------------------|------------------| ------- |
| `resources`*    | CmsResourceParams | информация о хендлере и его парамтрах в формате новой cms   | - | - |
| `resolversParams`*     | any               | любые параметры, которые надо заменить в параметрах ресурса | - | - |

\* - обязательные параметры

###Примечание:
параметры из ресурса могут содержать null как значение, такие значения выфильтровываются.
параметры из ресурса могут содержать значения вида `%%PARAMS.foo%%` Это указание на то, что это значение надо заменить
на значение такого же ключа из `resolversParams`, и если такого ключа не нашлось - удалить этот параметр из запроса


## Пример запроса
```bash
curl --location --request POST 'https://front-market-unified--marketfront-65641-initapi.demofslb.beru.ru/api/v1?gps=37.49453011558516%2C55.77339823403054&name=resolveCmsResource&dictionary=true&rearr-factors=test-resources' \
--header 'api-platform: IOS' \
--header 'X-Device-Type: SMARTPHONE' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": [
        {
            "resources": {
                "resolvers": [
                    {
                        "resolver": "resolveDJUniversalProducts",
                        "version": "v1",
                        "params": {
                            "djPlace": "discovery_lenta",
                            "billingZone": "default",
                            "page": 1,
                            "numdoc": 60,
                            "hid": null,
                            "hyperid": null,
                            "topic": null,
                            "range": "1",
                            "gaid": "%%PARAMS.gaid%%",
                            "cartSnapshot": "%%PARAMS.cartSnapshot%%",
                            "recomContext": null,
                            "widgetPosition": null,
                            "viewUniqueId": "%%PARAMS.viewUniqueId%%",
                            "showPreorder": true,
                            "rawParams": {
                                "parentPromoIds": [],
                                "shopPromoIds": [],
                                "nid": [],
                                "fromCMSFlagForRawParams": true,
                                "supplierIds": [],
                                "discountFrom": null,
                                "warehouseId": null
                            }
                        }
                    }
                ],
                "assembler": {
                    "type": "ProductSnippet"
                }
            },
            "resolversParams": {
               "viewUniqueId": "123"
            }
        }
    ]
}'
```
#Пример ответа
```json
{
    "results": [
        {
            "handler": "resolveAnyResource",
            "result": {
                "content": [
                    {
                        "title": "Конструктор Xiaomi MI ZJMH02IQI Colorful Fidget Cube",
                        "pictures": [
                            "https://avatars.mds.yandex.net/get-mpic/5209485/img_id8837606900998644524.jpeg/orig"
                        ],
                        "price": {
                            "value": 298,
                            "sign": "₽"
                        },
                        "rating": 4.51,
                        "opinionsCount": 54
                    },
                    {
                        "title": "Масса для лепки Play-Doh Мистер зубастик с золотыми зубами (F1259)",
                        "pictures": [
                            "https://avatars.mds.yandex.net/get-mpic/4120567/img_id2105163210278521706.jpeg/orig"
                        ],
                        "price": {
                            "value": 1560,
                            "sign": "₽"
                        },
                        "rating": 4.8,
                        "opinionsCount": 34
                    },
                    {
                        "title": "Геймпад Microsoft Xbox Elite Wireless Controller Series 2, черный",
                        "pictures": [
                            "https://avatars.mds.yandex.net/get-mpic/4984138/img_id5877289146505857881.jpeg/orig"
                        ],
                        "price": {
                            "value": 13110,
                            "sign": "₽"
                        },
                        "promocodeBadge": "-5%",
                        "rating": 4.43,
                        "opinionsCount": 134
                    }
                ]
            }
        }
    ],
    "collections": {}
}
```
