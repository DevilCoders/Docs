[![](https://yastatic.net/q/logoaas/v1/WFM-Frontend.svg?size=48)](https://wfm.taxi.yandex-team.ru)

|                           | teamcity | nanny | site                                                                                                       | 
|---------------------------| ------------- | ------------- |------------------------------------------------------------------------------------------------------------|
| **local yandex dev**      | – | – | [https://wfm.taxi.local.yandex.ru:1234](https://wfm.taxi.local.yandex.ru:1234)                             |
| **local yandex-team dev** | – | – | [https://wfm.taxi.local.yandex-team.ru:1234](https://wfm.taxi.local.yandex-team.ru:1234)                   |
| **remote dev**            | – | – | [wfm.%username%.front.taxi.dev.yandex-team.ru](https://wfm.%username%.front.taxi.dev.yandex.ru)            |
| **unstable**              | [teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomUnstable?branch=tef-wfm-frontend&buildTypeTab=overview) | [nanny-unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_wfm-frontend_unstable/) | [wfm.taxi.dev.yandex.ru](https://wfm.taxi.dev.yandex.ru)                                                   |
| **unstable-02**           | [teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomUnstable?branch=tef-wfm-frontend&buildTypeTab=overview) | [nanny-unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_wfm-frontend_unstable/) | [wfm-frontend-unstable-02.taxi.dev.yandex.ru](https://wfm-frontend-unstable-02.taxi.dev.yandex.ru)                              |
| **unstable-03**           | [teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomUnstable?branch=tef-wfm-frontend&buildTypeTab=overview) | [nanny-unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_wfm-frontend_unstable/) | [wfm-frontend-unstable-04.taxi.dev.yandex.ru](https://wfm-frontend-unstable-04.taxi.dev.yandex.ru) |
| **testing**               | [teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Customs_CustomTesting?branch=tef-wfm-frontend&buildTypeTab=overview) | [nanny-testing](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_wfm-frontend_testing/) | [wfm.taxi.tst.yandex.ru](https://wfm.taxi.tst.yandex.ru)                                                   |
| **stable**                | [teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Frontend_Monorepo_Releases_AutoRelease?branch=tef-wfm-frontend&buildTypeTab=overview) | [nanny-prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_wfm-frontend_pre_stable/) [nanny-stable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_wfm-frontend_stable/) | [wfm.taxi.yandex.ru](https://wfm.taxi.yandex.ru)                                                           |

## Запуск

### Локальный запуск Frontend-части

1. Смаунтить папку проекта из Аркадии  
Если нет локально арка, [дока на установку тут](https://docs.yandex-team.ru/devtools/intro/quick-start-guide). Также есть [FAQ по самым частым темам арка](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/projects/infrastructure-group/monorepo/).
```
mkdir -p /Users/$USER/arcprojects /Users/$USER/arc # если нет таких папок
arc mount --mount=/Users/$USER/arcprojects/tef-wfm-frontend --store=/Users/$USER/arc/tef-wfm-frontend-store --path-filter=taxi/frontend/services/tef-wfm-frontend
```

2. Скачать файлы из [yav](https://yav.yandex-team.ru/secret/sec-01fjeb8ag9afv1mp9bzzcbdn09). После скачивания обоих файлов, поменяйте расширение (просто допишите) на `.zip`.
3. Распаковать оба архива в папку tef-wfm-frontend/certs
4. В итоге должны быть `tef-wfm-frontend/certs/yandex.ru/(key|private).pem` и `tef-wfm-frontend/certs/yandex-team.ru/(key|private).pem`.
5. Запуск проекта локально делается двумя командами:
```shell
npm install
npm run start-local
```

#### Добавление нового хоста (локального или удалённого в проект)
Если вы добавляете новый хост (на дев машинке, локально другой порт запустили, добавили новое окружение и тд), нужно в [CORS конфиге](https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/CC_AUTHPROXY_CORS?name=CC_AU) добавить этот хост.   

### Стартовать серверную часть локально
1. Скачайте [файлы из yav](https://yav.yandex-team.ru/secret/sec-01f8w8mq8xetbc7397hcdftjxm/explore/versions) все файлы и положите в корень своего сервиса. **Для работы с сервером**
> yav мог их переименовать в TVM и ENV. Нужно переименовать их в корне репы `.tvm.json` и `.env` соответственно.

```bash
npm run start:server:local
```

Морда будет доступна по `https://wfm.taxi.local.yandex.ru:1234`

### Скачать index.html с новыми переводами локально
```bash
npm run start-local:load-static:local # скачает с локального сервера. Нужно запустить его сначала (см. ниже)
```

или

```bash
npm run start-local:load-static # скачает с тестинга. Стоит по умолчанию у старта локальной сборки
```

## Флоу работы и деплой

Описаны [здесь](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/flow/)

## Автогенерация типов с бекенда

`npm run typings — backend-py3:workforce-management`

_types.config.json_ - конфиг, в котором указывается из какого репозитория и сервиса брать yaml’ы ручек для генерации.

[репозиторий генератора](https://github.yandex-team.ru/ktnglazachev/taxi-typings)

## yandex-team

### Локально
Чтобы запустить локально сервис на домене yandex-team, достаточно в файле webpack.config.js закомментить одни строчки и раскомментить другие.  
Должно быть так, чтобы подменился домен:
```js
// ~19я строчка

{
    // ...
    // host: config.localHost,
    // For yandex-team account
    host: config.yandexTeamLocalHost,

    // key: fs.readFileSync('./certs/yandex.ru/private.pem'),
    // cert: fs.readFileSync('./certs/yandex.ru/key.pem'),
    // For yandex-team account
    key: fs.readFileSync('./certs/yandex-team.ru/private.pem'),
    cert: fs.readFileSync('./certs/yandex-team.ru/key.pem'),
}
``` 

## Полезные ссылки

* [Сервис в tariff-editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354810/info)
* [Бункер](https://bunker.yandex-team.ru/taxi-workforce-management/tanker)
* [Танкер](https://tanker.yandex-team.ru/project/wfm?branch=master)
* [Конфиг языков проекта](https://tariff-editor-unstable.taxi.tst.yandex-team.ru/dev/configs/edit/WFM_FRONTEND_UI_LANGUAGES?group=wfm-frontend)
* [Конфиг доменов сервиса](https://tariff-editor-unstable.taxi.tst.yandex-team.ru/dev/configs/edit/WFM_FRONTEND_DOMAINS?group=wfm-frontend)
* [Все конфиги wfm-frontend](https://tariff-editor-unstable.taxi.tst.yandex-team.ru/dev/configs?group=wfm-frontend)
