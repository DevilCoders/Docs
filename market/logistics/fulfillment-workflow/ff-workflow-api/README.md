Локальный запуск
------
1. Копируем стабовые проперти
Создать `servant-development.properties` из `servant-development.properties.dist` в той же папке

2. Поднимаем докер контейнеры.
`cd 'dependency-stubs' && docker-compose up -d`.

3. Выполнить миграции
`liquibase --url=jdbc:postgresql://localhost:15801/market_ff_workflow_local
--driver=org.postgresql.Driver
--username=market_ff_workflow
--password="market_ff_workflow"
--changeLogFile=changelog.xml
update`

если будет ошибка с отсутствием org.postgresql.Driver, указать путь к postgresql-42.2.5.jar:
`--classpath=postgresql-42.2.5.jar`

4. Запустить приложение из IDE со следущими параметрами:

Working directory:
```
ff-workflow-api
```

VM options:
```
-Denvironment=development
-Dspring.profiles.active=development
-Dlog.dir=logs
-Dconfigs.path=src/main/properties.d
```
Доп. настройка VM options для включения логирования в консоль:
```
-Dlog4j.configurationFile=src/main/conf/log4j2-development.xml
```

Доп. настройка VM options для включения логирования в файлы:
```
-Dlog4j.configurationFile=src/main/conf/log4j2.xml
```


Для профиля `development` TMS задачи не будут запускаться автоматически.
Подробности в [описании фреймворка](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/tms-core-quartz2).


### Интеграционные тесты.
Запуск из консоли - `ya make -DIT_TEST_SPLIT_FACTOR=1 -tt`

#### Что может пойти не так при запуске тестов из Идеи?
При запуске через `ya make -DIT_TEST_SPLIT_FACTOR=1 -tt`, берется максимальная версия библиотеки из classpath.
При запуске из Идеи берется первая попавшаяся версия, которая может быть устаревшей.
Таким образом, если при локальном запуске из Идеи наблюдаются странные ошибки, то надо
проверить, с какой версией соответствующей библиотеки запускается приложение в тестинге или проде
и с какой версией запускается тест, после чего задать нужную версию в `dependency.management.ya.make`
и закоммитить ее (также после этого надо сделать Regenerate Project: ya ide) из меню Build в Идее,
чтобы Идея подхватила изменение.

### Как узнать, какие версии библиотек попадут в classpath в тестинге и проде?
1. Сделать `ya make`;
2. Посмотреть в файле `ff-workflow-api-start.sh`, какая версия библиотеки попадает в команду, которая будет использована
для запуска приложения на тестинге и проде.

### Security
Security по умолчанию включено во всех окружениях.
Выключается добавлением параметра
VM options:
```
-Dsecurity.enabled=false
```


## О логировании и push-client

Json лог уходит через push-client в YT *(hahn.logs/market-fulfillment-workflow-log).*
Так как push-client читает файл логов периодически, то в момент ротирования мы можем потерять часть записей.

Тут описано как правильно ротировать логи с push-client:
[Принцип ротации файлов](https://wiki.yandex-team.ru/StatBox/GetLogsSystem#principrotaciilogovdljaixonlinezabora)

> Так как мы нечасто пользуемся логами в YT было решено пренебречь потерей логов.

Варианты решения ротировать через logrotate или перейти с push-client на Unified Agent

