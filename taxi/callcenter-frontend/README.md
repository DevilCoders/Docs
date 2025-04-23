[![oko health](https://badger.yandex-team.ru/oko/repo/taxi/callcenter-frontend/health.svg)](https://oko.yandex-team.ru/repo/taxi/callcenter-frontend)
[![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_TaxiCallcenterBuild)/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Ekbinfra_Taxi_TaxiCallcenterBuild)
[![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_ConfigNginxCallcenterFrontend)/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Ekbinfra_Taxi_ConfigNginxCallcenterFrontend)

### Запуск дев сервера в [QYP](https://qyp.yandex-team.ru)
- [Переезд в QYP](https://wiki.yandex-team.ru/taxi/web/yp-frontend-guide/)
- [Настройка tvmtool](/docs/tvmtool/readme.md)

### Описание проекта

Группа сервисов для коллцентров Яндекс.Такси.

### callcenter-beta (основной сервис сейчас)
Представляет собой несколько частей
1) Панель работы с телефонией
2) Формы заказа такси, оформления тикетов в саппорте (в будущем возможно появление других сервисов)
3) Внешняя админка скрытая за cc-authproxy.

### callcenter-trainer
Тренажер для формы заказа такси. Здесь операторы тренируются при найме и сдают экзамены

### Hosts
- Unstable
[phoneorderbeta-unstable.taxi.tst.yandex.ru](https://phoneorderbeta-unstable.taxi.tst.yandex.ru)
[phoneorderbeta-unstable.taxi.tst.yandex.ru/order](https://phoneorderbeta-unstable.taxi.tst.yandex.ru/order)
[phoneorderbeta-unstable.taxi.tst.yandex.ru/admin](https://phoneorderbeta-unstable.taxi.tst.yandex.ru/admin)
- Testing
[phoneorderbeta.taxi.tst.yandex.ru](https://phoneorderbeta.taxi.tst.yandex.ru)
[phoneorderbeta.taxi.tst.yandex.ru/order](https://phoneorderbeta.taxi.tst.yandex.ru/order)
[phoneorderbeta.taxi.tst.yandex.ru/admin](https://phoneorderbeta.taxi.tst.yandex.ru/admin)
- Production
[phoneorderbeta.taxi.yandex.ru](https://phoneorderbeta.taxi.yandex.ru)
[phoneorderbeta.taxi.yandex.ru/order](https://phoneorderbeta.taxi.yandex.ru/order)
[phoneorderbeta.taxi.yandex.ru/admin](https://phoneorderbeta.taxi.yandex.ru/admin)

**Get параметры запроса**

- `phone` - Телефон клиента
- `ll` - Город заказа такси
- `gfrom` - Название города, например Москва. Будет отображаться в поле Откуда
- `IDChain` - Id звонка в октелл

###Процесс работы
Основная ветка - develop.
Сервис представляет собой монорепозиторий.
В папке packages лежат общие пакеты. В папке services - сервисы.
Чтобы начать разработку нужно выполнить команду npm install в корне репозитория. Дальше смотри файлы readme.md в services для сервиса в котором нужно работать.

Например для callcenter-beta - https://github.yandex-team.ru/taxi/callcenter-frontend/blob/develop/services/callcenter-beta/readme.md

Пакет callcenter-scripts - общий пакет для сервера для всех сервисов. Если в нем делаются какие-то изменения, нужно патчить и публиковать версию перед деплоем сервиса.

### Процесс выкатки
Сервисы деплоятся в RTC.
https://teamcity.taxi.yandex-team.ru/project/YandexTaxiProjects_Frontend_CallcenterFrontend?branch=callcenter-beta&buildTypeTab=overview#all-projects


### Логи в админке

https://tariff-editor.taxi.yandex-team.ru/logs?status_code=5&type=/v1/orders/commit,/v1/orders/draft
https://tariff-editor.taxi.yandex-team.ru/logs?status_code=4&type=/v1/orders/commit,/v1/orders/draft,/v1/orders/search
https://tariff-editor.taxi.yandex-team.ru/logs?status_code=4&type=integration/orderscommit,integration/ordersdraft

### Танкер

https://tanker.yandex-team.ru/?project=taxi&branch=master&keyset=callcenter-frontend

### Бункер

https://bunker.yandex-team.ru/taxi-callcenter
