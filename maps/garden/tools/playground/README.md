# Garden playground tools

## Playground management tool

Живёт в поддиректории `cli`.

* `garden-playground setup` - создаёт новый плейграунд
* `garden-playground update` - обновляет докер-образ в плейграунде (останавливает запущенный плейграунд для обновления)
* `garden-playground run` - запускает плейграунд
* `garden-playground remove` - удаляет плейграунд
* `garden-playground upload` - заливает локальный бинарник огородного модуля в плейграунд в контур `<username>_test`

## UWSGI application

Живёт в поддиректории `uwsgi`.

Это Flask-сервис, который выводит список плейграундов, работающих на хосте.

## Сборка

При изменении файла `package/debian/changelog` CI автоматически запускает сборку deb-пакета.

CI: https://a.yandex-team.ru/projects/maps-core-garden/ci/actions/launches?dir=maps/garden/tools/playground&id=playground-flow
