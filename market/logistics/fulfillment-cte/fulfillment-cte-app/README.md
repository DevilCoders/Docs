Локальный запуск
------

1. Поднимаем докер контейнеры.
`cd 'dependency-stubs' && docker-compose up -d`.

2. Выполнить миграции
`liquibase --url=jdbc:postgresql://localhost:15801/market_ff_cte_local \
--driver=org.postgresql.Driver \
--username=market_ff_cte \
--password="market_ff_cte" \
--changeLogFile=changelog.xml \
update`

если будет ошибка с отсутствием org.postgresql.Driver, указать путь к postgresql-42.2.5.jar:
`--classpath=postgresql-42.2.5.jar`
Путь к postgresql можно найти в Project Structure -> Project Settings -> Libraries -> postgresql-42.2.5.jar

3. Запустить приложение из IDE со следующими параметрами:

VM options:
```
-Denvironment=development
-Dspring.profiles.active=development
-Dconfigs.path=<absolute_path_to_properties.d>
-D_cte=<absolute_path_to_categories_and_quality_matrix_folder>
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
2. Посмотреть в файле `fulfillment-cte-start.sh`, какая версия библиотеки попадает в команду, которая будет использована
для запуска приложения на тестинге и проде.

### Ошибки которые могут быть
1. Если проект не запускается из-за Solomon и выходит Connection refused с портом для Solomon то достаточно закомментить 
код где изпользуется Solomon в SolomonPushClient
2. Также могут возникнуть ошибки связанные с плейсхолдором {fulfillment-cte.categories.file}, нужно закомментить 
все места где он используется.
3. Если вдруг выходит ошибка после выполнения миграции с помощью Liquibase: 
`Specifying files by absolute path was removed in Liquibase 4.0. Please use a relative path or add '/' to the 
classpath parameter`. 
То достаточно напиcать путь для changelog.xml и postgresql-42.2.5.jar начиная с `fulfillment-cte`
