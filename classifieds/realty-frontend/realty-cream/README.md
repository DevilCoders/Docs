# realty-front-cream

Своя CRM для биздева и операторов колл-центра.

## Основная информация

| Service | URL                                                                                                             |
|---|-----------------------------------------------------------------------------------------------------------------|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-cream |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-cream                                                 |
| Grafana | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-cream            |

## Хосты

| Environment | URL |
|---|---|
| Testing | https://cream.test.vertis.yandex-team.ru/ <br> https://branch-${branch}.cream.test.vertis.yandex-team.ru/ <br> https://cream.test.vertis.yandex.net/ <br> https://branch-${branch}.cream.test.vertis.yandex.net/|
| Production | https://cream.vertis.yandex-team.ru/ <br> https://cream.vertis.yandex.net |

## Регистрация пользователя

### Если есть пользователь-администратор
Идём на тестинг, находим страницу регистрации в мёню, регистрируем при помощи формы

### Если нет пользователя
1. Идём на mail.yandex-team.ru, в url добавляется query параметр uid, копируем его
1. Идём в [свагер](http://yandex-realty-crm-api.vrts-slb.test.vertis.yandex.net/#!/users/upsertUserRoute) и регистрируем пользователя по этому uid
