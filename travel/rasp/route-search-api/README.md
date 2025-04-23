# route-search-api
Сервис поиска расписания транспортных средств от пукта A в пункт B на дату D.

## Qloud
[unstable](https://qloud-ext.yandex-team.ru/projects/rasp/experimental-route-search-api/unstable)
[testing](https://qloud-ext.yandex-team.ru/projects/rasp/experimental-route-search-api/testing)
[production](https://qloud-ext.yandex-team.ru/projects/rasp/experimental-route-search-api/production)

## Sandbox
[Пример задачи по сборке и деплою проекта в Qloud](https://sandbox.yandex-team.ru/task/308510790/view) 
[Пример задачи по генерации ресурса с данными](https://sandbox.yandex-team.ru/task/307477741/view)

## Teamcity
[Собрать и выкатить в Unstable](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Rasp_ExperimentalRouteSearcheApi_CreateNewDockerImageAndDeployToUnstable)

## Как начать разрабатывать
1) Качаете ресурс с данными
2) Разархивируете его в ./data/dumps
3) Затем компилируете проект
4) ./route-search-api --config config.json
5) Приложение подымется на localhost:9999

## Примеры запросов:
http://localhost:9999/api/bus-direction/?departure_point_key=c54&arrival_point_key=c11164&departure_date=

