# grid-yt-schemagen

Инструмент для генерации схемы YT-таблиц, с которыми работает новый интерфейс Директа

Запускать так:

    cd direct/libs/grid-yt-schemagen
    ya make
    ya tool java11 -classpath 'grid-yt-schemagen/*' -Djava.library.path=./grid-yt-schemagen/ ru.yandex.direct.grid.schemagen.GridSchemaGenTool -g $PATH_TO_GRID_SCHEMA

`$PATH_TO_GRID_SCHEMA` -- путь до ${ARCADIA_ROOT}/direct/libs/grid-yt-schema/src/main/java/

Для добавления нового класса представления таблицы:

1. Добавить запись в libs-internal/config/src/main/resources/common-production.conf, пример: (page: "//home/yabs/dict/Page")
2. Добавить метод в ru.yandex.direct.ytcomponents.config.DirectYtDynamicConfig (см. похожие в классе)
3. Добавить запись в ru.yandex.direct.grid.schemagen.sqlgen.YtSqlGenerator в методе getSchemas (см. похожие в методе)
4. Выполнить скрипт описанный выше.
