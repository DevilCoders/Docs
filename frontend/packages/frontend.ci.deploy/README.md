# @yandex-int/frontend.ci.deploy

Пакет для деплоя сервисов в beta и production окружения и удаления beta-окружений.

## Как подключить в сервис
Установить `@yandex-int/frontend.ci.deploy` последней версии.
В сервисе нужно создать файл по пути `.config/deploy/config.json`. Формат конфига следующий:
```(json)
{
    "type": "report-renderer" | "qloud" | "ydeploy" | "whatever",
    "beta": {}, // конфиг для beta-окружения
    "release": {} // конфиг для production-окружения
}
```
Типы конфигов уникальны для окружений и описаны в [документации](./docs) про деплой этих окружений.

Также возможно использовать *.js файлы для конфига. Обязательно `module.exports = { ... }` - этот объект должен быть идентичен формату конфига

## Поддерживаемые окружения
- [ReportRenderer (Yappy)](./docs/report-renderer.md)
- [QLoud](./docs/qloud.md)
- [YDeploy](./docs/ydeploy.md)


## Режимы деплоя (YENV)

При запуске `frontend-deploy deploy` (и `remove` тоже) необходимо установить переменную окружения `YENV`. Поддерживаются значения `testing` или `production`. Они влияют на то, какая часть конфига (`beta` или `release`) будет прочитана, и какой скрипт будет выполнен.

Запуск `YENV=testing frontend-deploy deploy` подходит для сборки пулреквестов в трендбоксе. В пути к бетам (`report-renderer`, `qloud`) используется номер пулреквеста (из переменной окружения `TRENDBOX_PULL_REQUEST_NUMBER`).

## Как добавить свой скрипт деплоя

Разработка скриптов ведется в директории deploy-scripts.
1. Нужно создать поддиректорию с названием нового типа деплоя (YDeploy, т.д.)
2. В `deploy-scripts/types.ts` в `DeployTypes` добавить этот новый тип деплоя.

3.  Создать директорию `deploy-scripts/{deployEnv}`. В ней нужно написать скрипты деплоя и тайпинги для конфига.
    В директории нового способа деплоя описать тайпинги для конфига и сами скрипты деплоя.
    При написании скрипта деплоя нужно отнаследоваться от класса [DeployScript](./src/deploy-scripts/base.ts) и переопределить пять методов
    - `getConfigType` - по типу из этого метода будет определено - запускать ваш скрипт или нет.
    - `deployBeta` - реализация скрипта деплоя в beta-окружение
    - `removeBeta` - реализация скрипта удаления beta-окружения
    - `deployRelease` - реализация скрипта деплоя в production-окружение
    - `createDraft` - реализация скрипта создания драфта окружения


    При написании тайпинга конфига нужно определить 3 поля в типе:
    - `type` - окружение для деплоя (`qloud`, `report-renderer`, т.д.)
    - `beta` - тип конфига для beta-окружений
    - `release` - тип конфига для production-окружений

4. В [deploy-scripts/index.ts](./src/deploy-scripts/index.ts) добавить созданные классы в нужные массивы и дополнить тип `DeployConfig` своим типом конфига через `|`:
`type DeployConfig = RRConfig | QloudConfig | NewConfig`
5. В [deploy-scripts/index.ts](./src/deploy-scripts/index.ts) импортировать созданный скрипт и добавить в массив скриптов, которые возможны для запуска

## Owners
- [platosha](https://staff.yandex-team.ru/platosha) - RR deploy; YDeploy; общие вопросы по библиотеке
- [jsus](https://staff.yandex-team.ru/jsus) - автор поддержки деплоя в YDeploy
- [an9eldust](https://staff.yandex-team.ru/an9eldust) - автор поддержки деплоя в Qloud
