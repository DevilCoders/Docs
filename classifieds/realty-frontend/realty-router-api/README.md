# realty-router-api

Сервис роутера Недвижимости.

## Основная информация

| Service | URL                                                                                                                  |
|---|----------------------------------------------------------------------------------------------------------------------|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-router-api |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-router |
| Grafana | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-router |

## Хосты

| Environment | URL |
|---|---|
| Testing | http://realty-front-router-http.vrts-slb.test.vertis.yandex.net <br> http://realty-front-router-${branch}-http.vrts-slb.test.vertis.yandex.net |
| Production | http://realty-front-router-http.vrts-slb.prod.vertis.yandex.net |

Чтобы посмотреть результат с прода на локальной машине нужно подкючиться по [h2p](https://wiki.yandex-team.ru/vertis-admin/h2p/)

---

## Построение урлов

URL: `http://realty-front-router-http.vrts-slb.test.vertis.yandex.net/link`

```bash
POST /link 

REQUEST:
    {
        "links": [
            {
                "name": <ROUTE_ID>,
                "viewType": "desktop" | "touch-phone"
                "params": {
                    ...
                }
            }
        ]
    }

---

RESPONSE: [ <link-1>, <link-2>, ... ]
```
### Пример:
```json
REQUEST:
    {
        "name": "newbuilding-search",
        "viewType": "desktop",
        "params": {
            "rgid": 587795,
            "type": "SELL",
            "streetId": "166746",
            "streetName": "sudostroitelnaya-ulica",
            "timeToMetro": 10,
            "metroTransport": "ON_FOOT"
        }
    }
```
```json
RESPONSE: 

    [
        "/moskva/kupit/novostrojka/st-sudostroitelnaya-ulica-166746/ryadom-metro/"
    ]
```
---

## Парсинг урлов

URL: `http://realty-front-router-http.vrts-slb.test.vertis.yandex.net/parse`

GET-параметры:
* `url` - урл для парсинга (нужно заэнкодить)
* `viewType` - платформа для роута (desktop | touch-phone)

```
GET `/parse`

$ curl 'http://realty-front-router-http.vrts-slb.test.vertis.yandex.net/parse?url=/moskva/kupit/kvartira/st-sudostroitelnaya-ulica-166746/s-bolshoy-kuhney/&viewType=desktop'
```

```json
RESPONSE:

    {
        "name": "search",
        "data": {
            "method": "GET",
            "directory": "pages/deskpad",
            "action": "build",
            "controller": "search",
            "react": true
        },
        "params": {
            "rgid": 587795,
            "type": "SELL",
            "streetId": "166746",
            "streetName": "sudostroitelnaya-ulica",
            "category": "APARTMENT",
            "kitchenSpaceMin": 10
        }
    }

```
