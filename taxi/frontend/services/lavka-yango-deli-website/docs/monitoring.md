# Мониторинг

## Графана
Графана позволяет изучать статы из nginx'а в виде графиков. Дефолтные графики - rps и timings. Статы агрегируются через [Dorblu](https://wiki.yandex-team.ru/taxi-infra/dorblu/?from=%2Fjandekskarty%2Fadmining%2Ftech%2Fdorblu%2F#vdvuxslovax).

* [Тестинговая графана](https://grafana.yandex-team.ru/d/AUbmQd9Mz/nanny_lavka_yango-deli-website_testing)
* * [Конфиг графаны](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/grafana/nanny_lavka_yango-deli-website_testing.yaml)
* * [Конфиг dorblu](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/dorblu/lavka/nanny.lavka_yango-deli-website_testing.yaml)
* [Продовая графана](https://grafana.yandex-team.ru/d/SCSWrOrGz/nanny_lavka_yango-deli-website_stable?orgId=1&refresh=30s)
* * [Конфиг графаны](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/grafana/nanny_lavka_yango-deli-website_stable.yaml)
* * [Конфиг dorblu](https://github.yandex-team.ru/taxi/infra-cfg-graphs/blob/master/dorblu/lavka/nanny.lavka_yango-deli-website_stable.yaml)

### Полезные ссылки
 
* [Графики и алерты](https://wiki.yandex-team.ru/taxi/frontend/grafiki-i-alerty/)
* [Графики, мониторинги, логи и алерты на фронтовый сервис](https://wiki.yandex-team.ru/taxi/frontend/mlu-frontend-talks/#vstrecha16.03.2021)

## Кибана
Кибана содержит логи, которые мы отправляем через src/service/logger.
В проде мы отправляем логи в tskv формате в stdin, эти логи перехватываются syslog-ng(конфиг лежит в etc/syslog-ng/conf-enabled/lavka-yango-deli-website.conf), откуда перехватываются пилорамой(сервис обработки и отправки логов) и попадают в кибану.

* [Тестинговая кибана](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(filters:!(('$state':(store:globalState),meta:(alias:!n,disabled:!f,index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',key:name,negate:!f,params:(query:yango-deli-website),type:phrase),query:(match_phrase:(name:yango-deli-website)))))&_a=(columns:!(_source),filters:!(),index:'1df0b0f0-b956-11e9-9ad8-afd09b0ebd4e',interval:auto,query:(language:kuery,query:''),sort:!(!('@timestamp',desc))))
* [Продовая кибана](https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(filters:!())&_a=(columns:!(_source),filters:!(('$state':(store:appState),meta:(alias:!n,disabled:!f,index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,key:name,negate:!f,params:(query:yango-deli-website),type:phrase),query:(match_phrase:(name:yango-deli-website)))),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:''),sort:!(!('@timestamp',desc))))

### Полезные ссылки

* [Пилорама](https://wiki.yandex-team.ru/taxi/backend/architecture/pilorama/)

## Error Booster
В [Error Booster'е](https://error.yandex-team.ru/projects/yango-deli-website) мы можем найти клиентские логи, которые мы отправляем через client/lib/error-logger.

### Полезные ссылки

* [Error Booster](https://wiki.yandex-team.ru/error-booster/)
* [Настройки Error Booster'a](https://error.yandex-team.ru/projects/yango-deli-website/settings)

## Алерты
Алерты осуществляются через juggler и приходят в телеграм каналы lavka-yango-alerts или lavka-yango-alerts-testing(только nginx алерты). У нас есть два источника алертов - логи error booster'a и nginx статы.

* Настройка алертов Error Booster'a осуществляется следующим образом - нужно изучить [доку](https://wiki.yandex-team.ru/error-booster/alerts/) по алертам, добавить нужные алерты на [странице](https://error.yandex-team.ru/projects/yango-deli-website/settings/alerts) Error Booster'a и затем на [странице](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3Dyango-deli) уведомлений Juggler'a.
* Настройка алертов по статам из nginx осуществляется следующим образом - нужно описать нужный телеграм канал в этом [файле](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/telegram_options), затем прописать какие алерты нужно тригерить в файлах конфигов для [тестинга](https://github.yandex-team.ru/taxi/infra-cfg-juggler/blob/master/checks/taxi.lavka.test/rtc_lavka_yango-deli-website_testing) и [прода](https://github.yandex-team.ru/taxi/infra-cfg-juggler/tree/master/checks/taxi.lavka.prod).


### Полезные ссылки

* [Juggler](https://juggler.yandex-team.ru)
* [Juggler документация](https://docs.yandex-team.ru/juggler/)
* [Графики и алерты](https://wiki.yandex-team.ru/taxi/frontend/grafiki-i-alerty/)
* [Графики, мониторинги, логи и алерты на фронтовый сервис](https://wiki.yandex-team.ru/taxi/frontend/mlu-frontend-talks/#vstrecha16.03.2021)
