# realty-front-payment

Платёжный iframe для ввода банковских карт через ЮMoney. По сути просто отдаёт html-ку с подключенным скриптом. Нужен для прохождения аудита PCI DSS.

Аппрувить и катить могут только те кто прошел обучение по PCI DSS:

https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/a.yaml

https://a.yandex-team.ru/arcadia/classifieds/services/maps/realty-front-payment.yml

## Флоу работы:
1. Создается PR. Для того чтобы его можно было вмержить необходим аппрув от одного из ответственных за сервис. Ответственный за сервис обозначен в файле a.yaml в корне realty-frontend ([роль Ревьюер платежной формы](https://idm.yandex-team.ru/system/abc/roles#f-role=abc/services/verticals/realty/*/6064,f-ownership=personal,f-status=active,sort-by=-updated)). Задача ответственного проверить что:
    - Код соответствует тикету
    - В коде отсутствуют уязвимости
    - Заведен тикет на аудит безопасности
2. Параллельно с этим происходит тестирование сервиса + проходит аудит безопасности с помощью формы: https://wiki.yandex-team.ru/product-security/audit/.
3. После мержа тикет выкатывается в тестинг.
4. При попытке выкатить из тестинга в прод будет необходим аппрув на выкатку от одного из ответственных за сервис. Ответственный должен убедиться, что:
    - Выкатываемая версия соответствует той, что связана с тикетом
    - К выкатке прикреплен верный тикет
    - Пройден аудит безопасности

## Основная информация

| Service    | URL |
|------------|---|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-payment |
| Deploy     | https://admin.vertis.yandex-team.ru/services/realty-front-payment |
| Grafana    | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-payment |

## Хосты

| Environment | URL |
|---|---|
| Testing | https://realty.test.vertis.yandex.ru/payment/ <br> https://branch-${branch}.realty.test.vertis.yandex.ru/payment/ |
| Production | https://realty.yandex.ru/payment/ |
