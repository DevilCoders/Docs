# compositor

https://abc.yandex-team.ru/services/compositor

## Релиз новой версии
`releaser release --buildfile docker_package.json`

Выкатка в прод
`releaser deploy -e production`

## Локальный запуск
собираем пакет `ya package docker_package.json --docker --docker-repository=tools`
Это нужно сделать один раз чтобы локально был образ (если изменились зависимости - нужно
пересобрать)

Далее `docker-compose up local` - на локалхосте поднимется сервис, если внести 
изменения в код - перезапускать не нужно, изменения тут же будут подтягиваться в 
запущенное приложение

## Запуск тестов

`ya make -ttt tests` в папке проекта
