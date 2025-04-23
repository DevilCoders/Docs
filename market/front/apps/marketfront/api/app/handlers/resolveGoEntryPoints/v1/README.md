# Резолвер resolveGoEntryPoints

Возвращает точки входа для интеграции с приложением Yandex Go. Точками входа являются страница поиска и категории
товаров, доступные для экспресс-доставки. Данные категории вовращаются не в нормализованном, а в специально
подготовленном виде. Так как данная ручка возвращает категории, доступные для экспресс доставки, то обязательным
параметром является gps координата в формате `<longitude>,<latitude>`.

_Нужно учесть, что идентификатор региона определяется не по gps координате, а берётся из stout_

## Параметры

Обязательный параметр _gps_.

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `gps` | string | gps координата в формате `<longitude>,<latitude>` | - | - | - |

## Пример запроса

```shell script
curl --request POST \                                                                                                                                                       [10:32:25]
 --url 'https://<FAPI_HOST>/api/v1?name=resolveGoEntryPoints' \
 --header 'Content-Type: application/json' \
 --data '{"params":[{"gps": "37.627144621768366,55.73965699105317"}]}' \
```

## Пример ответа резолвера

```json
{
  "results": [
    {
      "handler": "resolveGoEntryPoints",
      "result": {
        "search": {
          "url": "/yandex-go/entrypoint?gps=37.627144621768366%2C55.73965699105317"
        },
        "searchIntents": [
          {
            "name": "Зоотовары",
            "nid": 54496,
            "picture": "//avatars.mds.yandex.net/get-mpic/901948/img_id7637861564482752331.jpeg/orig",
            "url": "/yandex-go/search?nid=54496&gps=37.627144621768366%2C55.73965699105317"
          },
          {
            "name": "Электроника",
            "nid": 54440,
            "picture": "//avatars.mds.yandex.net/get-mpic/372220/img_id3015291950024439449/orig",
            "url": "/yandex-go/search?nid=54440&gps=37.627144621768366%2C55.73965699105317"
          }
        ]
      }
    }
  ],
  "collections": {}
}
```


## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/resolveGoEntryPoints/v1/index.js#)
