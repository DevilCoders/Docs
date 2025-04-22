### Локальный запуск тестов Darkspirit

Для тестов нужен `oracle instantclient` [инструкция и файлы](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html).
1. Завести virtualenv python2.7, установить зависимости из [requirements.txt](../docker/darkspirit/requirements.txt) и [requirements_dev.txt](../docker/darkspirit/requirements_dev.txt).
2. Выставить переменные окружения:
    ```bash
    export NLS_LANG="AMERICAN_CIS.UTF8"
    export ORACLE_HOME=... # путь до oracle_instantclient
    export TNS_ADMIN=... # путь до папки с tnsnames.ora
    export NLS_DATE_FORMAT="DD mon YYYY HH24:MI"
    export NLS_SORT="RUSSIAN"
    export NLS_LANG="AMERICAN_AMERICA.UTF8"
    export NLS_NUMERIC_CHARACTERS=". "
    ```
   Подробнее про tnsnames.ora по [ссылке](https://wiki.yandex-team.ru/spirit/darkspirit/#poluchitdostupkbd)
3. Научить ОС находить библиотечные файлы из `oracle instantclient`, например так:
    * Mac OS X: `export DYLD_LIBRARY_PATH="$ORACLE_HOME:$DYLD_LIBRARY_PATH"` 
    * Linux: `export LD_LIBRARY_PATH="$ORACLE_HOME:$LD_LIBRARY_PATH"`
    * Общее решение: поместить библиотечные файлы в стандартную для ОС директорию
4. Скопировать секреты для доступа в MDS из YaVault: [secrets](../secrets/README.md)

N.B. Тесты запускаются из корня репозитория командой `py.test tests --application-config-file $filename`. 
Из другой папки они не запускаются из-за проблем с путями, забитыми в тестах.

Специфику для запуска тестов поверх локальной БД читай в папке [docker](../docker/README.md).
