## Генерация проеекта для IDE

`ya ide idea --group-modules=tree -r="$HOME/arcadia/projects/marketId" --directory-based --yt-store`

`-r` - обязательный параметр, путь до директории, где будут хораниться файлы с проекстом (рекомендуется делать вне репозитория, чтобы не захламлять выдачу `status`)

`--directory-based` - формат IDEA проекта на основе директорий (позволяет сохранять настройки и конфигурации запуска между перегенерациями проекта)

`--yt-store` - кеш артефактов в YT (по задумке должен ускорять скачивание по сравнению с sandbox)

После выполнения команды и запуска проекта в IDEA убедитесь, что у вас установлена последняя версия Ya IDEA plugin
(путь до файла с плагином выводится в командную строку после выполнения `ya ide idea...`).

## Локальный запуск

### Локальный PG в docker

1. устанавливаем docker (если еще нет)
2. `docker pull postgres`
3. `mkdir -p $HOME/docker/volumes/postgres`
4. `docker run --rm --name pg-market_id-docker -e POSTGRES_PASSWORD=market_id -e POSTGRES_USER=market_id -d -p 5432:5432 -v $HOME/docker/volumes/postgres:/var/lib/postgresql/data postgres`

### Накатка liquibase

1. скачать `liquibase.jar` или для mac установить через homebrew (`brew install liquibase`) и актуальный драйвер PG
2. для локальной инсталяции PG можно использовать команду (указать корректный относительный путь от текущей директории
до jar файла с драйвером PG):
```
liquibase --changeLogFile=changelog.xml --driver=org.postgresql.Driver --url=jdbc:postgresql://localhost:5432/market_id --username=market_id --password=market_id --defaultSchemaName=public --logLevel=DEBUG --classpath='relative path to PG driver jar' update
```

### Настройка запуска приложения

1. Main class: `ru.yandex.market.marketId.Marketid`
2. VM options (указать значения для HTTP и GRPC портов):
`-Dconfigs.path=src/main/properties.d -Dhttp.port=<any http port> -Dgrpc.port=<any grpc port>`
3. Убедиться, что Working directory указываетMarketIdService на рут диретории marketId в аркадии (может отличаться, если мета файлы проекта лежат в другой директории)

![Настройка запуска приложения](https://jing.yandex-team.ru/files/sergey-fed/RunDebug_Configurations_2019-06-04_11-06-31.png "Настройка запуска приложения")

## Как сделать запрос к GRPC ручкам

1. для mac можно установить GRPC CLI через homebrew (`brew install grpc`)
2. получить список всех доступных сервисов - `grpc_cli ls localhost:<grpc-port> -l`
3. создать запись в market id:
```
grpc_cli call localhost:41501 ru.yandex.market.id.MarketIdService.getOrCreateMarketId --json_input --json_output '
{
  "partnerId": 1,
  "partnerType": "SHOP",
  "uid": 100,
  "contactId": 1000,
  "legalInfo": {
    "legalName": "test",
    "type": "abc",
    "registrationNumber": "4321",
    "legalAddress": "test address1",
    "physicalAddress": "test address 2"
  }
}'
```