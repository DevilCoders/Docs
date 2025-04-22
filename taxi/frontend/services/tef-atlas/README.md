[![](https://yastatic.net/q/logoaas/v1/Яндекс.Такси:%20Атлас.svg?size=48)](https://atlas.yandex-team.ru)

## Хосты
### dev

[taxi-atlas.%username%.front.taxi.dev.yandex-team.ru](//taxi-atlas.%username%.front.taxi.dev.yandex-team.ru)

### unstable

[teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomUnstable?branch=tef-atlas&buildTypeTab=overview)

[nanny-unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_atlas_unstable/)

[atlas-unstable.taxi.tst.yandex-team.ru](https://atlas-unstable.taxi.tst.yandex-team.ru)

### test

[teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomTesting?branch=tef-atlas&buildTypeTab=overview)

[nanny-testing](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_atlas_testing/)

[taxi-atlas.taxi.tst.yandex-team.ru](https://taxi-atlas.taxi.tst.yandex-team.ru)

### prod

[teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Releases_AutoRelease?branch=tef-atlas&buildTypeTab=overview)

[nanny-prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_atlas_prestable/)

[nanny-stable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_atlas_stable/)

[atlas.yandex-team.ru](https://atlas.yandex-team.ru)

## Сервис в админке 

[tariff-editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354298/info)

## Установка

- скачать архив с сертификатами из [yav](https://yav.yandex-team.ru/secret/sec-01g4f455x5nrh56hjjcc2kjhfp)
- распаковать архив в папку cert

## Запуск

На своей виртуалке из `/home/%username%/www`

> :information_source: Точно собирается под нодой 14.19.0

```
git clone git@github.yandex-team.ru:taxi/frontend-monorepo.git
cd frontend-monorepo/services/tef-atlas
npm i
```

### Локальный запуск

`npm run local`

### Стартовать статику в деве

`npm start`

### Стартовать ноду в деве (в проде сейчас не используется)

```
cd server
npm i
npm run start:dev
```

> :information_source: Подробнее на [wiki](docs/ServerComponent.md)

## Флоу работы и деплой

Описаны [здесь](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/flow/)

## Webpack-bundle-analyzer

```
с виртуалки

в вебпаке stats: 'normal'

npm run profile

грохнуть 2 первые строчки в stats.data.json

./node_modules/webpack-bundle-analyzer/lib/bin/analyzer.js stats.data.json --mode=static ./static/build

mv report.html www/report.html
```

## Я.Метрика

* [PROD](https://metrika.yandex.ru/dashboard?group=day&period=quarter&id=46322841&ulogin=ya-metrika)

Чтобы получить доступ, нужно получить в Управляторе роль "Менеджер Яндекса" в проекте "Метрика".

## Техническая документация

- [Автоматическая генерация типов](docs/typesGeneration.md)
