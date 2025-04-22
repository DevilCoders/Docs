# Статические страницы Маркета

## Адреса
### Балансеры, в которые нужно настраивать прокси
* Тестинг: `market-static-pages.tst.vs.market.yandex.net`
* Продакшн: `market-static-pages.vs.market.yandex.net`

### Маркет
* Продакшен `market.yandex.ru/thanks/`
* Тестинг `market.fslb.yandex.ru/thanks/`

### Маркет
* Продакшен `pokupki.market.yandex.ru/promo/*`
* Тестинг `desktop.pokupki.market.fslb.yandex.ru//promo/*`

## Сервисы

### Продакшен
* `production_market_static_pages_sas` (3 инстанса)
* `production_market_static_pages_msk` (3 инстанса)

### Тестинг
* `testing_market_static_pages_sas` (1 инстанса)
* `testing_market_static_pages_msk` (1 инстанса)

## Файловая структура и разработка
### Струкрутра
* `src` — исходники статических страниц, шаблоны.
* `src/marketplace-promo` — исходники промок Беру
* `public` — собранные страницы и статика
* `thanks` — маркетная страница ["Спасибо"](https://market.yandex.ru/thanks/), нужно перенсти по аналогии с другими страницами

### Разработка
Очень желательно иметь исходники каждого лендинга, поэтому требуйте их от подрядчиков (если делаете не сами). Складывайте их в `src` согласно структуре.

Так же желательно иметь предварительно подготовленную команду для сборки новой версии.
Например `npm release`, которая будет запускать компиляцию класть свежую версию в `public`.

*Как сделать хорошо*
```json
  "scripts": {
    "dev": "node dev/server.js",
    "prebuild": "rimraf ./htdocs",
    "build": "gulp build",
    "public:prepare": "rm -rf ../../../public/marketplace-promo/spasibo-na-beru",
    "public:copy": "cp -r ./htdocs ../../../public/marketplace-promo/spasibo-na-beru",
    "public:all": "npm run public:prepare && npm run public:copy && npm run prebuild",
    "release": "npm run prebuild && npm run build && npm run public:all"
  },
```

## Как выкатить изменения

1. Коммитим в репозиторий [https://github.yandex-team.ru/market/market-static-pages](https://github.yandex-team.ru/market/market-static-pages) (**ВНИМАНИЕ!!!** *изменения должны быть закоммичены вместе с собранным дистрибутивом, сборка при билде будет возможна после выполнения [этого](https://st.yandex-team.ru/CSADMIN-14614) таска*)
2. Клонируем и запускаем задачу `BUILD_MARKET_FRONT_STATIC` (ссылка на задачу в [sandbox](https://sandbox.yandex-team.ru/task/868133396/view)).
3. Релизим в тестинг (кнопка Release), в задаче появится ссылка на релиз реквест.
4. Дожидаемся пока все сервисы перейдут в состояние `DEPLOY_SUCCESS`.

## Конфигурация

[https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/front/market_static_pages](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/front/market_static_pages)

## Деплой

* Sandbox задача [https://sandbox.yandex-team.ru/task/868133396/view](https://sandbox.yandex-team.ru/task/868133396/view)
* Исходники [https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/market/sre/BuildMarketFrontStatic](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/market/sre/BuildMarketFrontStatic)

## История
([корневой таск](https://st.yandex-team.ru/MARKETVERSTKA-20719), [таск с деплоем](https://st.yandex-team.ru/CSADMIN-14470)).
