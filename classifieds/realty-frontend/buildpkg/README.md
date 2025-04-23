# realty-frontend-buildpkg

Docker-образ `registry.yandex.net/vertis/realty-frontend-buildpkg`
с предустановленными зависимостями для сборки пакетов фронта Недвижимости.

## Сборка

1. Обновить `CHANGELOG.md`
2. Закоммитить, после этого собрать через [TC](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=vs_frontend_Applications_AuroRuFrontendRepo_RealtyFrontendBuildpkg)
или выполнить `make` (сначала надо будет настроить докер и [залогиниться](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)

## Настройка TeamCity

Чтобы контейнер имел доступ к github.com (например, для npm-зависимостей),
надо его монтировать с опцией `-v /home/teamcity/.ssh:/home/teamcity/.ssh`
