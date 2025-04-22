# Виджеты для партнеров
[![Build Status](https://teamcity.taxi.yandex.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_TaxiWidgetBuild)/statusIcon)](https://teamcity.taxi.yandex.ru/viewType.html?buildTypeId=Ekbinfra_Taxi_TaxiWidgetBuild)

## Установка

В разметку необходимо добавить блок для виджета
```html
<div class="ya-taxi-widget"
    data-size="s"
    data-theme="normal"
    data-title="На&nbsp;такси в&nbsp;Цветной"
    data-point-b="37.589569560,55.733780"
    data-use-location="true"
    …
    ></div>
```

и скрипт виджета

- production
```
<script src="//yastatic.net/taxi-widget/ya-taxi-widget.js"></script>
```

- testing
```
<script src="//yastatic.net/taxi-widget/testing/ya-taxi-widget.js"></script>
```

- unstable
```
<script src="//yastatic.net/taxi-widget/unstable/ya-taxi-widget.js"></script>
```

## Поддерживаемые параметры

`data-hide-info` – скрывает иконку информации

`data-app` – иконка виджета и айдишник для метрики
* `2187871` – иконка янго

`data-size` – размер виджета
* `xs` – экстра маленький
* `s` – маленький
* `m` – большой (с картинкой)

`data-theme` – тема виджета
* `normal` – тема по-умолчанию
* `dark` – темная тема (пока есть только для большого виджета, использовать когда темная картинка на фоне)

`data-title` – название, например, `На&nbsp;такси в&nbsp;Цветной`

`data-description` – описание, например, `Цветной бульвар 15, стр 1`

`data-point-a` – координаты точки A (`long,lat`), например, `37.589569560,55.733780`

`data-point-b` – координаты точки B (`long,lat`), например, `37.589569560,55.733780`

`data-use-location="true"` – использовать определение местоположения пользователя (точка А), если параметр отсутствует, то не использовать

`data-proxy-url` — URL для проксирования перехода, например, через Метрику. Пример такого URL:

`https://3.redirect.appmetrica.yandex.com/route?start-lat={start-lat}&amp;start-lon={start-lon}&amp;end-lat={end-lat}&amp;end-lon={end-lon}&amp;gfrom={start-lat,start-lon}&amp;gto={end-lat,end-lon}&amp;utm_source=maps-api&amp;utm_medium=67cd5b9b899740a98f5437b2aca5e144&amp;appmetrica_tracking_id=1034000268724878793`

Поддерживаются подстановки: `{start-lat}`, `{start-lon}` (будут содержать пустые значения, если геолокация запрещена), `{end-lat}`, `{end-lon}`, а также комбинированные `{start-lat,start-lon}`, `{start-lon,start-lat}`, `{end-lat,end-lon}`, `{end-lon,end-lat}`.

`data-clid` – CLID партнера

`data-apikey` – ключ для авторизации

`data-tariff` – какой тариф запрашивать
* `econom` — «Эконом». Значение по-умолчанию.
* `business` — «Комфорт».
* `comfortplus` — «Комфорт+».
* `minivan` — «Минивен».
* `vip` — «Бизнес»

`data-req` – требования, перечисляются через запятую
* `yellowcarnumber` — машина с желтыми номерами.
* `nosmoking` — некурящий водитель.
* `childchair` — наличие детского кресла в машине.
* `bicycle` — перевозка велосипеда.
* `conditioner` — кондиционер в машине.
* `animaltransport` — перевозка животных.
* `universal` — машина-универсал.
* `check` — необходима квитанция об оплате.
* `ski` — перевозка лыж или сноуборда.
* `waiting_in_transit` — ожидание в пути.
* `meeting_arriving` — встреча с табличкой.
* `luggage` — платная перевозка багажа

`data-picture` – ссылка на картинку, для большого виджета (если не указать, загрузится карта)

`data-nonce` – nonce атрибут

`data-zoom` – zoom для карты, по-умолчанию 17

`data-custom-layout="true"` – кастомная разметка.

### Поля для кастомной разметки

`data-title="true"` – место для названия

`data-link="true"` – ссылка (проставляет нужный href)

`data-description="true"` – место для описания

`data-disclaimer="true"` – место для дисклеймера

## Debug
Скрипт добавляет в window объект YaTaxiWidget, который содержит информацию о скрипте
```
window.YaTaxiWidget.version; // process.env.VERSION
```

## Разработка
1. Запускаем локальное `npm run build`
2. Смотрим файл `open dev.html`

## Сборка
Для того чтобы собрать скрипт, необходимо выполнить команду:

```bash
npm run build
```

Итоговый скрипт будет лежать в директории `./dist`

## Локализация

Собирать переводы нужно во время разработки.

```npm run localization``` - подтягивает все переводы из танкера и кладет их в json.

## Версионирование

в dist лежат версии скриптов
-v1
-v2
-v*

при установке пакета создается копия ya-taxi-widget.js => на нужную версию скрипта

Согласованый подход к обновлению скрипта. Выкладывается новая версия скрипта v*, клиенты тестируют его,
в течении переходного периода ссылка ya-taxi-widget указывает на текущую версию. После истечения
переходного периода ссылка меняется на новую версию скрипта, а старая остается жить какое-то время, или
перманентно.

Версия скрипта поднимается в конфиге webpack + docker/stage.dockerfile.

## Публикация

- [Stable](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Releases_AutoRelease?branch=txf-taxi-widget&mode=builds)
- [Testing](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomTesting?branch=txf-taxi-widget&buildTypeTab=overview&mode=builds)
- [Unstable](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomUnstable?branch=txf-taxi-widget&buildTypeTab=overview)
