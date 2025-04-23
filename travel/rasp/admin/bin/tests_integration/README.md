Интеграционные тесты Админки.
https://st.yandex-team.ru/RASPFRONT-7494
https://st.yandex-team.ru/RASPADMIN-1018

Запускается Большой импорт (БИ) и переключение.
Запускаем БИ на небольшом наборе данных. При этом импорты идут из подготовленных заранее файлов.

Запуск тестов - через бинарник tests_integration.
Настройки по умолчанию - на машине должен быть mysql и mongo, с доступом от root без пароля.
Все временные файлы во время работы создаются прямо в директории, где находится бинарник.
Т.е. при наличии баз на машине, запуск ./tests_integration без параметров должен отработать.

Конфигурация - через переменные окружения. См. travel/rasp/admin/tests_integration/run.py IntegrationTests.__init__

Пример конфигурации:
```shell script
export Y_PYTHON_SOURCE_ROOT=$HOME"/work/arc/arcadia"
export PYTHONUNBUFFERED=1

export RASP_TESTS_MYSQL_NAME_DB1=rasp_integration_db1
export RASP_TESTS_MYSQL_HOST_DB1=127.0.0.1
export RASP_TESTS_MYSQL_PORT_DB1=3306
export RASP_TESTS_MYSQL_USER_DB1=rasp
export RASP_TESTS_MYSQL_PASSWORD_DB1=123

export RASP_TESTS_MYSQL_NAME_DB2=rasp_integration_db2
export RASP_TESTS_MYSQL_HOST_DB2=127.0.0.1
export RASP_TESTS_MYSQL_PORT_DB2=3306
export RASP_TESTS_MYSQL_USER_DB2=rasp
export RASP_TESTS_MYSQL_PASSWORD_DB2=123

export RASP_TESTS_MYSQL_NAME_MAINTENANCE=rasp_maintenance
export RASP_TESTS_MYSQL_HOST_MAINTENANCE=127.0.0.1
export RASP_TESTS_MYSQL_PORT_MAINTENANCE=3306
export RASP_TESTS_MYSQL_USER_MAINTENANCE=rasp
export RASP_TESTS_MYSQL_PASSWORD_MAINTENANCE=123

# опциональные флаги
export RASP_BI_CONTINUE=1 # Продолжить с последнего упавшего скрипта
export RASP_FORCE_NO_FLAG=1 # Снимает флаг проведения работ перед переключением
export RASP_TESTS_SKIP_INIT=1 # Пропуск начальной заливки базы
export RASP_TESTS_SKIP_BI=1 # Пропустить большой импорт и сразу перейти к переключению
```

Для [локального запуска](https://st.yandex-team.ru/RASPFRONT-8190) нужно установить [OAuth-токен](https://wiki.yandex-team.ru/sandbox/api/#oauth):
```shell script
export SANDBOX_OAUTH_TOKEN=<token>
```

Also need ~/.yt/token for https://a.yandex-team.ru/arc_vcs/travel/rasp/library/python/common/apps/im_logs/models.py?rev=r8223419#L94
