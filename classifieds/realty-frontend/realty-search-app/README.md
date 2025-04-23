# realty-front-search-app

Это nodejs-приложение для:
* встраивания вертикали Недвижимости в Поисковое Приложение (ПП) Яндекса
* ручки для блока Недвижимости на веб морде Яндекса

## Основная информация

| Service | URL |
|---|---|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-search-app |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-search-app |
| Grafana | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-search-app |
---
## Хосты

| Environment | URL |
|---|---|
| Testing | https://search-app.realty.test.vertis.yandex.ru <br> https://branch-${branch}.search-app.realty.test.vertis.yandex.ru|
| Production | https://search-app.realty.yandex.ru |
---
## Разработка

* `make start-local` -  запуск

## Ручка для объявлений (o.yandex.ru)

* прод: https://search-app.realty.yandex.ru/api/classified/data?geo_id=213&platform=desktop&limit=10&imgSize=272x272&imgSizeRetina=450x450
* тестинг: https://search-app.realty.test.vertis.yandex.ru/api/classified/data?geo_id=213&platform=desktop&limit=10&imgSize=272x272&imgSizeRetina=450x450
* дев: https://realty-frontend.search-app.realty.{{login}}.dev.vertis.yandex.ru/api/classified/data?geo_id=213&platform=desktop&limit=10&imgSize=272x272&imgSizeRetina=450x450

Для корректной работы необходимо указать заголовок x-yandexuid: <number>Yandexuid
