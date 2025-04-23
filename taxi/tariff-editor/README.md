# Яндекс.Такси - Админка 3.0

| Pull request checks | Unstable | Testing | Stable |
| :-------------------- | :--------------: | :-------------: | ----------: |
| [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_TariffEditorProject_TariffEditorCheckArc)/statusIcon)](https://teamcity.taxi.yandex-team.ru/buildConfiguration/Ekbinfra_Taxi_TariffEditorProject_TariffEditorCheckArc?mode=builds#all-projects) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_TariffEditorProject_TariffEditorUnstableArcadia)/statusIcon)](https://teamcity.taxi.yandex-team.ru/buildConfiguration/Ekbinfra_Taxi_TariffEditorProject_TariffEditorUnstableArcadia) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_TariffEditorProject_TariffEditorTestingArcadia)/statusIcon)](https://teamcity.taxi.yandex-team.ru/buildConfiguration/Ekbinfra_Taxi_TariffEditorProject_TariffEditorTestingArcadia?mode=builds) | [![Build Status](https://teamcity.taxi.yandex-team.ru/app/rest/builds/buildType:(id:Ekbinfra_Taxi_TariffEditorProject_TariffEditorStableArc)/statusIcon)](https://teamcity.taxi.yandex-team.ru/buildConfiguration/Ekbinfra_Taxi_TariffEditorProject_TariffEditorStableArc?mode=builds) |

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=taxi/tariff-editor&vcs=arc)](https://oko.yandex-team.ru/arc/taxi/tariff-editor)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=taxi/tariff-editor&vcs=arc)](https://oko.yandex-team.ru/arc/taxi/tariff-editor)

### Запуск в development

`npm run init && npm run run`

Чтобы запустить на виртуалке без доступа во внешний интернет нужно убрать из зависимостей puppeteer

### Запуск в development отдельных пакетов и бандлов 

`npm run run -- pkg1:bundle1:bundle2 pkg2 ...` например
`npm run run -- cars services:antifrod` соберет весь пакет Авто и пакет Сервисы с единственным разделом Антифрод

будет работать только после хотя бы одной полной сборки

### Workflow

- создаем новый бранч
- когда считаем что можно выдать на тестирование - вешаем на пулреквест метку `taxi/tariff-editor/unstable`
- [запускаем в teamcity сборку unstable откружения](https://teamcity.taxi.yandex-team.ru/buildConfiguration/Ekbinfra_Taxi_TariffEditorProject_TariffEditorUnstableArcadia) 
- когда фича протестирована в unstable, создаем PR в `master`, предварительно по возможности слив все изменения в один коммит
- далее читаем [про релизы](https://a.yandex-team.ru/arcadia/taxi/tariff-editor/docs)

_Unstable окружение создаётся на базе ветки stable, далее к ней подмердживаются все пулреквесты в лейблом unstable_

### Тестинг

Домен yandex-team нужен, чтобы передавать куки в API.

- NGINX - [config-nginx-taxi-tariff-editor](https://github.yandex-team.ru/taxi/config-nginx-taxi-tariff-editor)
- unstable - https://tariff-editor.taxi.dev.yandex-team.ru
- dev - https://tariff-editor.{USER}.front.taxi.dev.yandex-team.ru
- testing - https://tariff-editor.taxi.tst.yandex-team.ru
- prestable - https://tariff-editor-prestable.taxi.yandex-team.ru
- stable - https://tariff-editor.taxi.yandex-team.ru

### RTC

- Прод: https://tariff-editor-rtc.taxi.yandex-team.ru
- Тест: https://tariff-editor-rtc.taxi.tst.yandex-team.ru
- Анстейбл: https://tariff-editor-rtc.taxi.dev.yandex-team.ru

### Документация

* [wiki Практики и правила написания кода в Админке](https://a.yandex-team.ru/arcadia/taxi/tariff-editor/docs)
* [wiki описание тарифов](https://wiki.yandex-team.ru/users/liumin/konstruktor-tarifov/)
* [wiki API админки](https://wiki.yandex-team.ru/taxi/backend/api/admin/)

### Мониторинги

- [Голован](https://yasm.yandex-team.ru/panel/robot-taxi-clown.nanny_taxi_tariff-editor_stable)
- [Кибана](https://kibana.taxi.yandex-team.ru/goto/0703d638e815c1dc2b96aa986a3fcb02)
- [Error](https://error.yandex-team.ru/projects/tariff-editor)
- [RUM](https://rum.yandex-team.ru/projects/tariff-editor)
- [LightHouse](https://tariff-editor.taxi.tst.yandex-team.ru/frontend-performance)
- [Деплои](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354285/deployments)

### ENV

`export PATH=/opt/nodejs/8/bin:$PATH`

### API

переключаться между апи так, ввести в консоли браузера

-  ```__adminConfig.setApi('api-t')``` - тестинг
- ```__adminConfig.setApi('api-u')``` - анстейбл

посмотреть список доступных апи

 ```__adminConfig.getAvailableApi()```

доступно везде, кроме прода

### Застрял релиз, но нужно выкатить отдельную задачу

Можно черепикнуть нужный коммит в релизную ветку, которая в проде, и выкатить новый релиз хотфиксом.
- arc co trunk
- arc co -b {release-branch}-fix
- arc cherry-pick {commit}
- arc push ...
- arc pr create
Подробнее про хотфиксы [тут](https://a.yandex-team.ru/arcadia/taxi/tariff-editor/docs/8.4-build-hotfix.md).

### Notes

handsontable использует внутри numbro, который ломается в продакшн сборке на версии numbro@2.1.2 (https://github.com/BenjaminVanRyseghem/numbro/issues/402)
