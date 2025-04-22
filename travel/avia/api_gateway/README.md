# api-gateway

Описание: https://wiki.yandex-team.ru/avia/flight-storage/avia-api-gateway/

## Методы

### Получение информации о рейсе (/flight)

Url: `/flight/<company_iata>/<flight_number>/?departure_day=<YYYY-MM-DD>`

Дополнительные параметры:
- lang -- язык, например "ru" или "en"
- fields -- запросить дополнительные данные:
- flight_status -- получить статус рейса из shared-flights
- flight_rating -- получить рейтинг рейса из avia-backend

## Мониторинг

### Голован

- [testing](https://yasm.yandex-team.ru/template/panel/avia-api-gateway/;env=testing)
- [load](https://yasm.yandex-team.ru/template/panel/avia-api-gateway/;env=load)
- [production](https://yasm.yandex-team.ru/template/panel/avia-api-gateway/;env=production)

## Разработка

```
$ cp ./tools/samples/environments.sh ./tools/environments.sh
$ vi ./tools/environments.sh
$ ./tools/run-dev.sh
```

## Разработка в pycharm
* Запускаем `ya make -t` чтобы собрались необходимые бинари
* Заходим в `Preferences -> Project -> Project Interpreter`
* Выбираем путь до интерпретатора `${ARCADIA_ROOT}/travel/avia/api_gateway/tools/python`
* Для tornado-server.py настраиваем окружение. Например так:
```shell script
cp ./tools/samples/local.env ./tools/local.env
vi ./tools/local.env
# и добавляем в EnvList
```

Работать должен и Run и Debug и тесты в pycharm. Если есть проблемы инструкция https://i-dyachkov.at.yandex-team.ru/1

## Сборка

```
$ ./ya package --checkout --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/api_gateway/pkg.json

$ cp ./docker/dev_env.list.sample ./docker/dev_env.list
$ vi ./docker/dev_env.list
$ docker run --env-file=docker/dev_env.list -it registry.yandex.net/avia/api-gateway:unstable /bin/bash
```
