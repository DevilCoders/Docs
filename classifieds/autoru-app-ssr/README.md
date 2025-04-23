# autoru-app-ssr

Сервис для server-side-rendering шаблонов для аппов iOS и Android

* **Прод**: `https://ssr.apiauto.ru`
* **Тестинг**: `https://ssr.autoru-api.test.vertis.yandex.net`

Доступные эндпоинты (во все ручки VIN-отчетов можно передавать как `vin_or_license_plate`, так и `offer_id`):
* `/1.0/android/makeXmlForOffer?offer_id=<...>`
* `/1.0/android/makeXmlForReport?vin_or_license_plate=<...>`
* `/1.0/android/makeXmlForSearch?vin_or_license_plate=<...>`

* `/1.0/ios/makeXmlForOffer?offer_id=<...>`
* `/1.0/ios/makeXmlForOfferPreview?offer_id=<...>`
* `/1.0/ios/makeXmlForReport?vin_or_license_plate=<...>`
* `/1.0/ios/makeXmlForSearch?vin_or_license_plate=<...>`

* `/1.0/ios/makeXmlForGarageLanding`
* `/1.0/ios/makeXmlForGarageCard?card_id=<...>`


Из входящего запроса в publicapi прокидываются следующий заголовки:
```
user-agent
x-android-app-version
x-authorization
x-client-date
x-device-uid
x-features
x-session-id
x-timezone-name
x-uid
x-vertis-platform
x-ya-user-ticket-vertis
x-yandex-expflags
```

Пример запроса:
```shell
$ curl -sv 'https://ssr.autoru-api.test.vertis.yandex.net/1.0/android/makeXmlForSearch?vin_or_license_plate=Z7G244000BS038157' -H 'x-authorization: swagger'
```

## Разработка

* [Сервис в shiva](https://admin.vertis.yandex-team.ru/services/autoru-app-ssr)
* [Сборка в Аркадии](https://a.yandex-team.ru/projects/autoru/ci/releases/timeline?dir=classifieds%2Fautoru-app-ssr&id=autoru-app-ssr)
* [Дашборд в Графане](https://grafana.vertis.yandex-team.ru/d/PuyL1eCMk/ssr-apiauto-ru)

### Требования

* nodejs v14. Проверяем `node --version`
* npm v6. Проверяем `npm --version`
* protoc v3. Установить можно через `brew install protobuf` или скачать из [официальной репы](https://github.com/protocolbuffers/protobuf)

### Сборка и запуск в деве

* клонируем репу
* `npm ci` (установка зависимостей)
* `npm run build` (первоначальная сборка)
* `npm run start` (запуск веб-сервера)
* сервер поднимается на порту 8080

В соседней вкладке можно запустить автоматическую пересборку изменённых файлов `npm run build:watch`

### CLI для генерации результирующего xml

* `npm ci` (установка зависимостей)
* `npm run build` (первоначальная сборка)

После этого можно запускать CLI, которые прогоняет JSON-mock без похода в реальный сервер.
```sh
$ node ./dist/src/bin/generate.js --method android.makeXmlForReport --mock mock.json
```

* Методы называются так же как и в API.
* `mock.json` - это JSON-файл соответствующий интерфейсу
```typescript
interface VinReportWithEnrichData {
    report: RawVinReportResponse;
    enrichData?: VinReportEnrichData;
}
```
В простом виде это может быть
```json5
{
    "report": {/* Чистый ответ от publicapi */}
}
```

### Тесты

Юнит-тесты пишутся на [jest](https://jestjs.io).

* Запуск всех тестов `npx jest`
* Запуск тестов в файле или папке `npx jest src/server/tmpl/ios/v1/cells/RepairCell.test.ts`

**ВАЖНОЕ ЗАМЕЧАНИЕ**: в jest есть snapshot'ы и есть соблазн их использовать везде.
На самом деле - это антипаттерн.
Важно понимать, что снэпшоты - это чистый дамп, поэтому такие тесты очень хрупкие и постоянно ломаются.
Хорошим паттерном будет иметь несколько e2e-снэпшотов для проверки общего выхлопа SSR.
А конкретные части выдачи в разных случаях лучше проверять напрямую без снэпшотов.

### Автосборка и выкатка PR в тестинг

При создании PR происходит автосборка и выкатка в тестинг в отдельный "бранч" в shiva.
Бранч называется так же как и ветка в git.
Он не заменяет и не влияет на общий тестинг.
При желании бранч можно выкатить и в прод.

Чтобы гарантированно попасть в бранч, надо к запросу добавить заголовок `x-branch-name: <название ветки>`
```
$ curl -sv 'https://ssr.autoru-api.test.vertis.yandex.net/ping' -H 'x-branch-name: AUTORUAPPS-15870'

# В ответе приходит версия приложения и бранч
< x-autoru-app-id: autoru-app-ssr=5d390f3
< x-autoru-branch: AUTORUAPPS-15870
```

### Моки ответов для автотестов

Мокировать ответы пабликапи можно через [mountebank](http://mockritsa-autoru-app-ssr-api.vrts-slb.test.vertis.yandex.net/).

Пример:
1. Создаем мок в moutebank (пример лежит прямо в репе)
```shell
$ curl -s 'http://mockritsa-autoru-app-ssr-api.vrts-slb.test.vertis.yandex.net/imposters' --data @examples/imposter.json
```
2. В ответе придет номер порта
```json5
{
    "protocol": "http",
    "port": 35947,
    "numberOfRequests": 0,
    "recordRequests": false,
    "requests": [],
    "stubs": [
        /* .... */
    ]
}
```
3. Теперь можно сделать запрос в приложение и передать туда этот номер в заголовке `x-mockritsa-imposter`. В этом случае приложение пойдет не в пабликапи, а заберет ответ из мока.
```shell
$ curl -sv 'https://ssr.autoru-api.test.vertis.yandex.net/1.0/android/makeXmlForSearch?vin_or_license_plate=Z7G244000BS038157' -H 'x-authorization: swagger' -H 'x-mockritsa-imposter: 35947'
```
