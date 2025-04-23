# CDP-INTAPI
Приватное (внутреннее) API CDP.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-intapi` - HTTP сервер обрабатывающий запросы(в большинстве своём - REST API).
Существует для решения 2х задач:
1. Предоставления информации необходимой для работы frontend-а Метрики
2. Интеграции с другими сервисами. Как внутри отдела Аналитических продуктов, так и со смежными командами в Яндексе

### Как сделать запрос?
production доступен через балансер `cdp-intapi.mertika.yandex.net`.

testing доступен через балансер `cdp-intapi.test.metrika.yandex.net`.

Аутентификация в `cdp-intapi` происходит с помощью TVM токена

Подробнее про балансеры тут - TBD


### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-intapi-production

testing - https://deploy.yandex-team.ru/stages/cdp-intapi-test

### Основные составные части
Сейчас cdp-intapi выполняет ровно одну полезную функцию: предоставления информации необходимой для работы frontend-а Метрики.
Конкретно это всевозможная информация для работы сегментатора для гридя клиентов в интерфейсе Яндекс.Метрики

Данные для сегментатора (помимо тех что генерируются статически из кода) формируются в соответствие со схемой, созданной
через Schema API в `cdp-api`. Описание `cdp-api` -  https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-api/README.md

## Графики

[Графики запросов к `cdp-intapi.metrika.yandex.net`](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=cdp-intapi.metrika.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=cdp-intapi.metrika.yandex.net;signal=service_total;?range=604800000)
