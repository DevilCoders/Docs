## Описание placeholders в запросе yql
    %(DATE_FROM) - дата с которой нужно отбирать данные (включительно)
    %(DATE_TO) - дата до которой нужно отбирать данные (не включительно)
    %(PREV_DATE_TO) - вчера по отношению к %(DATE_TO)
    %(RESULT_TABLE_FOLDER) - путь в YT к таблице с результатами сверки или импорта
    %(RESULT_TABLE_NAME) - имя таблицы с результатами.
        Для корректной работы не рекомендуется добавлять суффиксы и префиксы непосредственно в YQL-запросе,
        вместо этого необходимую информацию указывать в поле ResultTable (напр. table/%(TIME_WINDOW_UNIT)/%(DATE_FROM))
    %(FIRST_COMPONENT_NAME) - наименование первой сверяемой компоненты
    %(SECOND_COMPONENT_NAME) - наименование второй сверяемой компоненты
    %(FIRST_COMPONENT_TABLE_PATH) - полный путь к таблице с данными первой сверяемой компоненты
    %(SECOND_COMPONENT_TABLE_PATH) - полный путь к таблице с данными второй сверяемой компоненты
    %(COMPONENT_NAME) - наименование компоненты для импорта
    %(COMPONENT_TABLE_PATH) - полный путь к таблице с данными компоненты для импорта
    %(TIME_WINDOW_UNIT) - eдиница измерения временного окна

## Настройки IDEA
##### Корректное отображение кириллицы в properties
`Settings -> File Encodings -> Transparent native-to-ASCII conversion`

## Разработка
Разработка ведется в arc.

Собрать проект:
```bash
alias ya-idea='~/arcadia/direct/bin/ya-idea'
cd ~/arcadia/market/checker
ya-idea
```

### Локальный запуск
Создать конфигурацию:
```
Main class: ru.yandex.market.checker.MarketChecker
Working dir: папка проекта
VM options:
-Djava.library.path=/home/.../IdeaProjects/arcadia-market_checkers/dlls
-Djna.library.path=/home/.../IdeaProjects/arcadia-market_checker/dlls
-Denvironment=development
-Dlog4j2.contextSelector=org.apache.logging.log4j.core.async.AsyncLoggerContextSelector
-Dlog.dir=/tmp
-Dconfigs.path=/home/.../arcadia/market/checker/src/main/properties.d
-Dlog4j.configurationFile=/home/.../arcadia/market/checker/src/main/conf/local/log4j2-test.xml
-Dspring.profiles.active=development
```

Jetty стартует на 8081 порту, переопределить можно так:
1. создать properties по пути `src/main/properties.d/development`
2. прописать там:
```
http.port=8081 # порт для http запросов
```
