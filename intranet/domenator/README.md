# Domenator

## Ссылки
 - https://abc.yandex-team.ru/services/domenator
 - https://deploy.yandex-team.ru/projects/tools_domenator_back

## Выпуск новой версии
 - `ya tool releaser release` - собрать и выкатить в тестинг
 - `ya tool releaser deploy --stage domenator-prod` - катнуть потом в прод

 Хочу выкатить руками:
 - удобнее это делать через dctl - https://wiki.yandex-team.ru/deploy/docs/dctl
 ```
 ya tool dctl get stage domenator-test > domenator_test.yaml
 # внести нужные правки в конфиге
 ya tool dctl put stage domenator_test.yaml
 ```

 Если нужно зарелизить без changelog:
 - `ya tool releaser build --version <version>` - собрать докер образ
 - `ya tool releaser push --version <version>` - запушить docker-образ в репозиторий
 - `ya tool releaser deploy --version <version>` - выкатить в Y.Deploy

## Подключится к базе
 Зайти в контейнер по ssh и выполнить `dbshell`

## Открыть shell
 Зайти в контейнер по ssh и выполнить `shell`
 Если нужно с базой поработать в шеле - нужно вызвать
 ```
 from intranet.domenator.src.manage import *
 await bind_db()
 ```

 После чего можно работать с базой -
 ```
 from intranet.domenator.src.db import Domain
 await Domain.query.gino.all()
 ```
 В будущем унести это в инициализацию шелла - DIR-9262


## Миграции
 Настроено автоматическое обнаружение изменений в моделях

 Локально
 ```
 ya make migrations # собрать бинарник
 migrations/domenator-db revision --autogenerate -m 'message' # сделать новые миграции
 добавить новые файлики в migrations/ya.make и закоммитить их

 migrations/domenator-db upgrade head # накатить их локально
 ```

 Накатить потом в тестинге/проде - зайти в контейнер по ssh и
 ```
 ./domenator-db -c migrations/alembic.ini upgrade head
 ```
Важно!!! Для прода выкатываем сначала на хост `console` и там выполняем миграцию, иначе если будет выкачено на api/workers будут ошибки

## Запуск тестов
 `ya make -ttt tests`


## Запуск тестов через Pycharm
1. Создать файл `python` в папке `tests` и сделать `chmod +x python`
Его содержимое:
```
#!/bin/sh
export Y_PYTHON_SOURCE_ROOT=<путь до корня арка вида /Users/login/.../arcadia>
export Y_PYTHON_ENTRY_POINT=":main"
#export NO_MIGRATE_DB=True
export PYCHARM_TEST_RUN=True
<путь до корня арка вида /Users/login/.../arcadia>/intranet/domenator/tests/intranet-domenator-tests "$@"
```
2. Запустить хотя бы раз любой тест через ya make -t (чтобы у вас появился бинарь) - если он есть
запускать не нужно (нужно будет перезапускать только раз если зависимости обновятся)
3. Поставить постгресс локально если еще нет https://postgresapp.com/
4. Подключится к базе выполнить:
```
create database domenator;
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


## Полезное

### Замечание про соединения
Соединения в приложении ленивые - получаются из пула на первый запрос
и возвращаются в конце запроса.
Если есть потребность в длительной задаче, которая не требует дальнейшего
взаимодействия в базой - можно (нужно) отпустить соединение через
`await request['connection'].release(permanent=False)`
