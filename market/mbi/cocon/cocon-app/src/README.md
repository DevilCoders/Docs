##Java-sec 2.0

###Обновление зависимостей
1. `./ya make market/mbi/cocon`
2. `./ya ide idea --iml-in-project-root -lr ~/IntellijIdeaProjects/cocon market/mbi/cocon`

###Запуск тестов
1. `./ya make market/mbi/cocon -tt`

###Локальный запуск из Idea
Поднимаем PG локально в докере
```$bash
mkdir -p $HOME/docker/volumes/postgres/cocon
docker run --rm --name pg-cocon-docker -e POSTGRES_PASSWORD=cocon -e POSTGRES_USER=cocon -d -p 5432:5432 -v $HOME/docker/volumes/postgres/cocon:/var/lib/postgresql/data/ postgres
```

В папку `properties.d/local` стоит положить файл, заканчивающийся на `-local.properties`, например
```
01_secrets-local.properties:
cocon.tvm.secret=<сюда утянуть секрет от market_mbi_cocon_dev>
cocon.arcanum.api.token=<из yav.yandex-team.ru>

```
Секреты:
 - TVM - [market_mbi_cocon_dev](https://abc.yandex-team.ru/services/mbidevops/resources/?show-resource=8647671)
 - ST API - [mbi-components-test](https://yav.yandex-team.ru/secret/sec-01d7kp1kt0074hfqcnqps7v8xp/explore/versions)


Далее запускаем main class `ru.yandex.market.cocon.Cocon`

####Настройка запуска приложения
```
VM Options: -Dlogging.config=src/main/conf/local/log4j2-test.xml
Environment variables: PROPERTIES_DIR=src/main/properties.d
Working directory: $MODULE_WORKING_DIR$
Active profiles: local,development
```
