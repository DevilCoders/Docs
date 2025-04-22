# Админка единого хранилища

## Общий обзор

`app/` -  папка с flask-admin приложением

`docker/` -  папка со всем тем, что попадает в docker-образ

`tests/` - папка с тестами для автосборки

`tools/` - папка с инструментами для разработки

### app/

#### Как это работает

Flask сам по себе можно запустить на dev-сервере через app.run(), но поскольку
это dev-сервер, то мы его не используем, а используем gunicorn. Запускается это
всё следующим образом: в `ya.make` корня админки прописан запуск точки входа
gunicorn `travel.avia.shared_flights.admin.app.app:gunicorn` в котором в свою
очередь происходит импорт wsgi модуля `travel.avia.shared_flights.admin.app.wsgi`.

За информацией по сборке питона в аркадии идём 
[cюда](https://wiki.yandex-team.ru/arcadia/python/pysrcs/)

Итоговый бинарник принимает все те же параметры командной строки, что и gunicorn.
Запуск в контейнере производится через supervisor 
(`docker/supervisor/10-yandex-shared-flights-admin.conf`), где для конфигурации
в бинарник передаётся параметр 
`--config=python:travel.avia.shared_flights.admin.app.gunicorn_conf`
который берёт gunicorn конфигурацию из одноименного модуля.

## Для запуска

```
cd $ARC_ROOT/travel/avia/shared_flights/admin

cp tools/samples/environments.sh tools/
vim tools/environments.sh

./tools/run-dev.sh
```

## Для сборки в docker

```
cd $ARC_ROOT/travel/avia/shared_flights/admin

ya package --docker --docker-repository=avia pkg.json
```
В конца вывода можно увидеть название образа и его версию

## Перед тем как закомитить

Нужно локально прогнать тесты

```
cd $ARC_ROOT/travel/avia/shared_flights/admin
ya make -tt
```

Если всё подозрительно хорошо - не забудьте проверить, что все тесты доступны
для автосборки через `RECURSE` или `RECURSE_FOR_TESTS`, а также что сами тесты
включены в `TEST_SRCS`.