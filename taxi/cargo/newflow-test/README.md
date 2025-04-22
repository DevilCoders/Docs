Setup
=====

Для работы нужна утилита `tvmknife` или `ya`.

```sh
# You can use taxi-python3

taxi-python3 client.py --help

# Or setup your of virtualenv:

sh setup-env.sh
./.venv/bin/python client.py --help
```

Установка tvmknife
==================

Ubuntu:

```sh
yandex-passport-tvmknife
```

На остальных системах можно поставить ya tool:

https://wiki.yandex-team.ru/yatool/


Тестирование 1-1
==================

```sh
   python3  client.py  -p +7xxxxxxxxx
```
Тестирование Лавки
==================

```sh
   python3  client.py --lavka-client -p +7xxxxxxxxx --case create-only
```

Тестирование бачей
==================

```sh
   python3  client.py  -p +7xxxxxxxxx --batch-client --claims 2
```

Чтобы точки старта/назначений были немного разбросаны, можно добавить флаг `--randomize-pickup-coordinates` или `--randomize-dropoff-coordinates`

Параметры запроса
==================

Типовые запросы лежат в директории requests в корне проекта.

```sh
python3  client.py  -p +7xxxxxxxxx --request=requests/payment_on_delivery/partial_delivery.json
```

Информация о маршрутном листе/сегмента
==================

По waybill-у

```sh
   python3  tool.py logistic-dispatch/d4f270f9-5c00-45ad-8c07-1ae7e9cbc9a4
```

По Сегменту-у

```sh
   python3  tool.py --segment 29dc596d-40b0-4921-92db-46900152a477
```

Создать водителя
==================

```sh
   python3  create_profile.py --type auto
```

Автотесты
==================

ТГ чат с отчетами: https://t.me/joinchat/amrSB7aYNn5mODdi

Полезные ссылки
===============

https://wiki.yandex-team.ru/taxi/backend/logistics/dokumentacija/taximeter-emulator/
https://github.yandex-team.ru/taxi/taximeter-emulator
