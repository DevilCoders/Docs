# train_api
Бэкенд для поездов

## Быстрый старт
Проект лежит в Аркадии, поэтому для старта лучше использовать `arc`. Начало работы с `arc` https://wiki.yandex-team.ru/arcadia/arc/docs/setup/

Тесты можно запускать локально. Для этого нужно зайти в папку с Аркадией и дальше в папку ``travel/rasp/train_api``.
Запускаеем `ya make -tt`.

Плагин для PyCharm + arc https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/README.md

## Пулл-реквесты (ревью-реквесты)
Важно! Имя ревью должно содержать имя таска в стартреке. Потому что для сбора ченджлога используется фильтр по очередям в стартреке.

Примерный воркфлоу работы над задачей:
```shell script
arc checkout trunk
arc pull trunk
arc checkout -b TRAINS-xxx-something-about-task  ## xxx нужно заменить на номер тикета

# правим файлы

arc add file1 file2 ...
arc commit -m 'TRAINS-xxx описание таска или суть изменений'
arc pr create --push --no-edit

# правим файлы по резултатам ревью

arc add file3 file4 ...
arc commit -m 'TRAINS-xxx суть правок'
arc push
```

## Сборка/деплой docker-образа
Сборка и деплой происходят в релизной машине https://rm.z.yandex-team.ru/component/rasp_train_api

Конфиг сборки docker-образа https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/train_api/pkg.json

Конфиг Релизной Машины https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/release_machine/components/configs/rasp/train_api.py

## Собрать докер образ локально руками
Нужно прописать версию в ```pkg.json```, и в этом же файле поменять ```name``` c ```train-api``` на ```rasp/train_api```.
Далее, собрать докер образ и залить его в regestry.

Скрипт:

Нужно установить переменную окружения ``TRAIN_API_VERSION`` и запустить из корня проекта:
```shell script
perl -p -i -e 's/"name": "train-api",/"name": "rasp\/train-api",/' ./pkg.json
perl -p -i -e 's/"version": ".*?",/"version": "$ENV{TRAIN_API_VERSION}",/' ./pkg.json
~/work/arc/arcadia/ya package ./pkg.json --docker
# docker push registry.yandex.net/rasp/train-api
```

## Настройка дев стенда

### 1. Поднять виртуалку в QYP (если ещё нет)

https://wiki.yandex-team.ru/travel/rasp/dev/prepare-dev-stand/#1.1sozdaniemashinyvqyp

### 2. Собрать бинарник

```shell script
ya make
```

### 3. Собрать статику для django-debug-toolbar

```shell script
Y_PYTHON_SOURCE_ROOT=$(pwd)/../../../ \
  Y_PYTHON_ENTRY_POINT="travel.rasp.train_api.app:manage" \
  DJANGO_SETTINGS_MODULE=settings \
  bin/app/app collectstatic
```

### 4. Запустить gunicorn

```shell script
Y_PYTHON_SOURCE_ROOT=$(pwd)/../../../ \
  REQUESTS_CA_BUNDLE=<путь до локального https://crls.yandex.net/YandexInternalRootCA.crt> \
  DJANGO_SETTINGS_MODULE=settings \
  bin/app/app --bind=[::]:8000 --timeout=0
```

`--timeout=0` нужен, чтобы gunicorn не отвечал таймаутом на медленных запросах.

## Запуск manage.py shell
``DJANGO_SETTINGS_MODULE=travel.rasp.train_api.docker.local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.train_api.app:manage /app/app shell``

Где `/app/app`, - это бинарник нашего приложения, с путем до него. Допустимо указывать как полный путь, так и относительный.

## Скрипты
Скрипты запускаем так, на примере export_orders_and_refunds:

``DJANGO_SETTINGS_MODULE="travel.rasp.train_api.docker.local_settings" Y_PYTHON_ENTRY_POINT="travel.rasp.train_api.app:script" /app/app export_orders_and_refunds --min_date 2019-10-01 --max_date 2019-10-03 --orders_out /tmp/orders-01-10-2019.csv --refunds_out /tmp/refunds-30-10-2019.csv``

Для того, чтобы это работало прописываем в app.py скрипт по аналогии с export_orders_and_refunds.
Фукция, которая прописана в качестве основной для скрипта, должна сама разбирать аргументы коммандной строки.

## Другие полезности
Инструкция расписаний по переезду в Аркадию https://wiki.yandex-team.ru/raspisanija/move-project-to-arcadia/

Джанго в Аркадии https://wiki.yandex-team.ru/intranet/dev/python/org/arcadia/manual/djangotoarcadia/

Про разработку и дебаг PyCharm + Arcadia https://st.yandex-team.ru/DEVTOOLS-2353#5da58206a2b79e001e5d6663

## Проблемы, которые могут встретиться

1. Не отображается кнопка "Выбрать место" (отображается "Купить у УФС").
Возможно устарела БД, нужно убедиться, что БД свежая.

2. Не проходит бронирование?
Возможно нет активных контрактов, их можно сделать так:

``DJANGO_SETTINGS_MODULE=travel.rasp.train_api.docker.local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.train_api.app:manage /app/app dev_make_active_contracts``

## Индексы в mongodb
Недостающие индексы создаются при старте приложения, если установлена переменная окружения `RASP_MIGRATION_ALLOWED`.

В продакшене такую переменную окружения лучше выставить только на миграционном инстансе.
Поскольку на миграционном индексе приложение при выкатке не запускается,
то для создания недостающих индексов можно запустить:

``DJANGO_SETTINGS_MODULE=travel.rasp.train_api.docker.local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.train_api.app:manage /app/app shell``

Также на любом инстансе для создания недостающих индексов можно выполнить команду:

``DJANGO_SETTINGS_MODULE=travel.rasp.train_api.docker.local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.train_api.app:manage /app/app ensure_mongo_indexes``
