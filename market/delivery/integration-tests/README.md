# delivery-integration-tests
Интеграционные тесты WMS, Фулфилмента и Yard

[Ссылка на wiki](https://wiki.yandex-team.ru/delivery/fulfilment/testirovanie-wms-i-ff/avtotesty/)
____
## Запуск локально с генерацией отчета

Обычно делается из консоли примерно так:

`ya make -ttt  -F *wms.tests.selenium.receiving* --allure=allure-results/report`

Фильтр для запуска может быть любым, например `*wms.tests.selenium.order.OrderNewTest*`

Но нужно помнить о том, что фильтр должен трактоваться однозначно, потому как к примеру фильтр `*wms*` запустит все тесты в проекте т.к. это слово содержится в пути самого проекта.

Можно запускать тесты по test suites:
- они лежат в `src/test/java/ru/yandex/market/delivery/deliveryintegrationtests/wms/suites`

Пример фильтра дла запуска suite транспортейшена для мультитестинга - `*wms.suites.multitesting.TransportationTestSuite*`
____
## Что проверяют
1. Регресс FFWF
<br>Запускаются автоматом в пайплайне FFWF

2. Регресс WMS
<br>Запускается в пайплайнах сервисов WMS и на мультитестингах

3. Регресс Yard
<br>Запускаются автоматом в пайплайне Yard
