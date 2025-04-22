# frontend-shiva-hooks
Хуки для деплоя шивы.

* [Приложение в shiva](https://admin.vertis.yandex-team.ru/services/frontend-shiva-hooks)
* [Сборка в Arcadria](https://a.yandex-team.ru/projects/vsinfr/ci/releases/timeline?dir=classifieds%2Ffrontend-shiva-hooks&id=frontend-shiva-hooks)
* [Логи](https://grafana.vertis.yandex-team.ru/goto/MVnNLvrGz)

## Для сервисов auto.ru, префикс имени сервиса af-
Умеет создавать PR из релизной ветки и ставить метки `branch:<ENV>`.

Для того, чтобы хук отработал, надо в userMetadata выкатки добавить специальную строку
```
DEPLOY_HOOK create_pr=<repository>:<release_branch>:<maste_branch> (add_labels=release) (add_branch_label)
```
`add_labels=<label1>,<label2>` - Опционально. Добавляет метки к PR, метки разделяются череез `,`.

`add_branch_label` - Опционально. Добавляет метку с бранчем `branch:<ENV>` (например, `branch:testing`, `branch:stable`).

Например,
```
DEPLOY_HOOK create_pr=autoru-frontend:AUTORUFRONT-16063:master add_labels=release add_branch_label
```
После выкатки хук создаст в репозитарии `autoru-frontend` PR из ветки `AUTORUFRONT-16063` в `master`. Так же к PR будет добавлена метка `release`(`add_labels=release`) и метка `branch:testing`(`add_branch_label`)


Файлик с хуками для запуска тестов в TC: https://github.com/YandexClassifieds/frontend-shiva-hooks/blob/master/server/app-with-autotests.js

## Для сервисов Объявлений, префикс имени сервиса gf-

Запускает автотесты для соответствующего сервиса через хаб и передает параметры для сборки.

Для того, чтобы хук отработал, надо в userMetadata выкатки добавить строку
```
DEPLOY_HOOK autotest param1=value1 paramN=valueN
```
где `paramN=valueN` - параметры сборки.

В итоге пост запросом дернется урл вида `https://hub.vertis.yandex.net/v0/teamcity/build?buildTypeId=Verticals_Testing_General_WebTests&branch=master&paramN=valueN`, который запустит билд автотестов.

Список урлов тестов, соответствующих сервисам находится в `server/handlers/general/testBuildUrls.js`
