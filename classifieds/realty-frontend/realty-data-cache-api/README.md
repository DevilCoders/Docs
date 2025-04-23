# realty-data-cache-api

Сервис для получения закешированных ссылок для блоков на Яндекс.Недвижимости.

Тип сервиса - service 

Пока что отдаются ссылки для футера на Яндекс Недвижимости для страниц типа: search, search-categories, index.

## Основная информация
| Service | URL |
|---|---|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-data-cache-api |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-data-cache-api |
| Grafana | https://grafana.vertis.yandex-team.ru/d/zTp8d_Lnk/realty-data-cache-api?orgId=1&var-ENV=Prometheus-testing&var-dc=All |

## Хосты

| Environment | URL |
|---|---|
| Testing | http://realty-front-dc-api-http.vrts-slb.test.vertis.yandex.net |
| Production | http://realty-front-dc-api-http.vrts-slb.prod.vertis.yandex.net |

## Получение ссылок футера

URL: `http://realty-data-cache-api-http.vrts-slb.test.vertis.yandex.net/links`

GET-параметры:
* `rgid` - ргид (обязательный)
* `type` - тип сделки (по умолчанию SELL)
* `category` - тип недвижимости (по умолчанию APPARTMENT)

```
GET `/links`

$ curl 'http://realty-data-cache-api-http.vrts-slb.test.vertis.yandex.net/links/?rgid=497490&type=RENT&category:ROOMS'
```

```json
RESPONSE:



```
