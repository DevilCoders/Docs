# Яндекс.Директория API

[Документация для разработчика директории](https://github.yandex-team.ru/pages/yandex-directory/yandex-directory/docs/docs_dev.html)

[Документация для потребителя API](https://api-internal.directory.ws.yandex.net/docs/)


## Новый релиз

**В первый раз** нужно
* Пройти [по ссылке](https://wiki.yandex-team.ru/tools/dev/qloud/docker/) и настроить docker registry, если вы ещё этого не сделали
* настроить [релизер](https://github.yandex-team.ru/tools/releaser/blob/master/README.md)
* в `~/.bash_profile` написать `export DOCKER_TOKEN="твой токен для кулауда"`, и сделать `. ~/.bash_profile`

## Последовательность действий для обновления версии
 1. Написать в #connect-back "Собираю релиз"
 2. Пройтись по всем тикетам в статусе "Протестировано" и смерджить их
 3. Переключиться на trunk и сделать ```arc pull```
 4. Собрать новый релиз и выкатить на тестовый стенд(internal-test)
    ```
    ./release.sh test
    ```
 5. Проверить корректность новой версии на тестовом стенде(internal-test)
 6. Написать в чатик #connect-release и выкатить новую версию на прод (сразу на internal-prod и external-prod)
    ```
    ./deploy.sh prod
    ```

## Cобрать контейнер можно так

    $ releaser build --buildfile docker_package.json

Собрать и запушить

    $ releaser build --buildfile docker_package.json
    $ releaser push --buildfile docker_package.json
    $ ./deploy.sh -e some_env -v some_tag

## Запуск тестов

    $ ya make -ttt -AF functional.yandex_directory.core.cloud.tests.py::ClassName::test_name tests/

### Интеграция с PyCharm

PyCharm умеет пробрасывать локальные изменения на удаленный сервер https://jing.yandex-team.ru/files/chapson/screencast_2019-05-31_14-55-17.mp4. Чтобы это работало стабильно, рекомендую подключаться к сети не по WiFi, а по кабелю. Если это не работает, у вас проблемы с IPv6, обратитесь к ребятам в команде.

## Запуск тестов через Pycharm
1. Создать файл `python` в папке `tests` и сделать `chmod +x python`
Его содержимое:
```
#!/bin/sh
export Y_PYTHON_SOURCE_ROOT=<путь до корня арка вида /Users/login/.../arcadia>
export Y_PYTHON_ENTRY_POINT=":main"
export ENVIRONMENT="autotests"
#export NO_MIGRATE_DB=True
export PYCHARM_TEST_RUN=True
export PYTHONPATH="${PYTHONPATH}:<путь до корня арка вида /Users/login/.../arcadia>/intranet/yandex_directory/tests"
<путь до корня арка вида /Users/login/.../arcadia>/intranet/yandex_directory/tests/intranet-yandex_directory-tests "$@"
```
2. Запустить хотя бы раз любой тест через ya make -t (чтобы у вас появился бинарь
по пути `intranet/yandex_directory/tests/intranet-yandex_directory-tests`) - если он есть
запускать не нужно (нужно будет перезапускать только раз если зависимости обновятся)
3. Поставить постгресс локально если еще нет https://postgresapp.com/
4. Подключится к базе выполнить:
```
create database ydir_main;
create database ydir_meta;
create role ydir WITH SUPERUSER CREATEDB CREATEROLE LOGIN;
```
5. Указать файлик `python` как [system interpreter](https://jing.yandex-team.ru/files/i-dyachkov/Screen%20Shot%202019-09-12%20at%208.22.06%20PM.png)

6. Указать корень [аркадии в Working Dir](https://jing.yandex-team.ru/files/smosker/2020-04-09_12-23-36.png)

7. Сделать `Pytest` [Default Tests Runner](https://jing.yandex-team.ru/files/i-dyachkov/Screen%20Shot%202019-09-12%20at%208.25.58%20PM.png)

8. Попробовать запустить [любой тест через Pycharm](https://jing.yandex-team.ru/files/smosker/2020-04-09_12-34-56.png)
должен пройти

9. Раскоментить строчку `#export NO_MIGRATE_DB=True` в файлике `python`
это позволит не тратить при каждом запуске несколько секунд на проверку все ли
миграции накачены.

10. Пользоваться. Если появились новые миграции - закоментить строчку выше и запустить тест
любой чтобы накатились миграции.

### Если выше инструкция не работает
1. Подготовьте eggs и run configuration по [инструкции](https://wiki.yandex-team.ru/users/griganton/arcadiapythondebug/)
2. Задайте переменные `REMOTE_DEBUG_EGG_PATH`, `REMOTE_DEBUG_PORT` у себя -
   на них `conftest.py` триггернет `settrace()` в фикстуре.
4. В pycharm ловите свое приложение.

## ssh в контейнер

    $ releaser ssh -c backend -e internal-test -a directory
