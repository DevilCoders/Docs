## Как использовать базовый образ
Описано здесь: https://wiki.yandex-team.ru/taxi-ito/baseqloudimage/

## Как пересобрать базовый образ
С помощью команды `make`. Образ будет запушен в registry.yandex.net в репозиторий /taxi/baseimages/taxi-base-qloud-xenial с двумя тэгами:
`latest`
`текущий таймстемп`, полученный из `date '+%Y%m%d%H%M%S'` в момент сборки
