API фулфилмента для магазинов

## Локальный запуск
1. Необходимо предварительно локально поднятом postgres выполнить `src/liquibase/local/local_db.sql`
2. Запускать `Ff4Shops.java`, указав
  - Environment variable `PROPERTIES_DIR` со значением  - путь до директрии properties.d
  - VM option `-Dspring.profiles.active=local` для автоматического применения liquibase
3. Запускается параллельно и ff4shops-api (http-интерфейс), так и ff4shops-tms (cron-таски)

## Обновление зависимостей
1. `./ya make  --checkout market/mbi/ff4shops`
2. `./ya ide idea --iml-in-project-root -lr ~/IntellijIdeaProjects/ff4shops ~/svn/arcadia/market/mbi/ff4shops`

## Запуск тестов
1. `./ya make  --checkout market/mbi/ff4shops -tt`

Начиная с IDEA 2020.3, при сборке могут возникать проблемы с процессором библиотеки mapstruct. Лечится добавлением опции`-Djps.track.ap.dependencies=false` в File | Settings | Build, Execution, Deployment | Compiler | Build process VM options

## Настройка postgres в YC

Необходимо перейти в [YC](https://yc.yandex-team.ru/), затем в кластер **ff4shopsTestDb**, и выбрать базу данных.

Можно использовать текущую ([ff4shopsDevDb](https://yc.yandex-team.ru/folders/fooitpdeb3jtqsjoq87f/managed-postgresql/cluster/00ddcfe1-d984-4609-bc2c-7e5657ed9591?section=databases)), либо создать новую.

Для подключения надо скопировать следующие свойства в `src/main/properties.d/local/00_application-local.properties`:

```
DB_URL (master ноды) => ff4shops.datasource.master.url
DB_URL (replica ноды) => ff4shops.datasource.readonly.url
DB_USER => ff4shops.datasource.username
DB_PASS => ff4shops.datasource.password #(здесь надо ввести, поскольку пароль скрыт)
```

Также, в `ff4shops.datasource.url` надо добавить в конец _url_ параметр `prepareThreshold=0`, поскольку _postgres_ в _YC_ не обрабатывает  _JDBC prepared statements_.
