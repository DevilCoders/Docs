### Яндекс.Директория

В текущей документации описываются все ньюансы разработки Яндекс.Директории.

* [Багтрекер](https://st.yandex-team.ru/DIR)
* [Исходники](https://github.yandex-team.ru/yandex-directory/yandex-directory)

Исходный код документации хранится в файле `docs/docs_dev.md`.

Для рендеринга html файла из исходной markdown разметки нужно запустить следующую команду:

    $ make build_docs

Чтобы автоматически рендерить html файл на каждое изменение `docs_dev.md`:

    $ pip install watchdog
    $ make watch_docs

#### Документация API

Документация API представляет из себя документацию для конечных потребителей (клиентов) API, предоставляемого директорией.

Если вы поднимаете свой разработческий инстанс, то доки по нему будут
доступны по урлу типа `http://yd-dev.cmail.yandex.net:8009/docs/`,
где порт надо будет поменять на тот, что за вами закреплен.

Общую документацию мы пишем в файле `docs/index.md`.

Для того, чтобы дока перестраивалась на-лету, нужно просто зайти на страницу с документацией.

В проекте используется модуль [flask-swagger](https://github.com/gangverk/flask-swagger),
который автоматически генерирует спецификацию для Swagger Playground.

В случае возникновения каких-либо проблем, стоит сверяться со
[Swagger Specification](https://github.com/swagger-api/swagger-spec/blob/master/versions/2.0.md).
В этом документе есть информация про то, как правильно описывать
разные виды параметров, которые могут принимать ручки API.

### Style guide

В процессе написания кода мы стараемся следовать заветам [PEP8](http://www.python.org/dev/peps/pep-0008/) и [PEP257](https://www.python.org/dev/peps/pep-0257/),
однако внутри команды приняты дополнительные соглашения.

#### Запятая после элемента

После каждого элемента списка (словаря, множества, аргументов функции), размещенного на отдельной строке,
полагается ставить запятую. Это распространяется и на случаи с единственным элементом коллекции.

Да:

    d = {
        'hello': 'Hello',
        'world': 'World',
    }
    l = [
        10,
    ]

Нет:

    l = [
        10
    ]
    d = {
        'hello': 'Hello!',
        'world': 'World'
    }

Делается это не просто так: без запятой в конце коллекции добавление каждого нового элемента
приводит к изменению двух строчек исходного кода (запятая на предыдущей строчке и новый элемент),
в то время как с уже установленной запятой можно обойтись одной.

Со стороны выглядит "экономией на спичках", но сильно улучшает читаемость и сокращает объемы diff-ов внесенных изменений.

#### Двойные и одинарные кавычки

Двойные кавычки допускаются только при оформлении докстрингов (`"""`), во всех остальных
случаях строковые литералы должны быть заключены в одинарные кавычки (`'`).

Да:

    def hello():
        """Тестовая функция."""
        print 'Hello, you silly world!'

Нет:

    def hello():
        '''Тестовая функция'''
        print "Hello, you silly world!"

#### Докстринг без unicode

Да:

    def hello():
        """Тестовая функция"""

Нет:

	def hello():
	    u"""Тестовая функция"""

Мы знаем, что это является нарушением [PEP257](https://www.python.org/dev/peps/pep-0257/). Deal with it.

#### Переносы строк в блоках

Если в списке (словаре, множестве) содержится более одного элемента,
то необходимо "развернуть" его, оформив каждый элемент на отдельной строке.

Да:

    {
        'hello': 'Hello!',
        'world': 'World',
        'inner: {
            'embedded': 'value',
        }
    }
    dict(
        hello='world',
        world='hello',
    )
    my_brand_new_very_long_list_name = [
        'first_item_of_my_list_with_very_long_name',
        'second_item_of_my_list_with_very_long_name',
        'third_pretty_long_item'
    ]

Нет:

    my_list = ['first_item_of_my_list_with_very_long_name', 'second_item_of_my_list_with_very_long_name',
    'third_pretty_long_item']
    {'a': 1, 'b': 2, 'inner: {'embedded': 'value',}}
    dict(a=1, b=2, c=3, d=4)


#### Порядок импортов

Все импорты должны быть упорядочены следующим образом:

* Блок `from __future__ import ....`
* Блок стандартной библиотеки.
* Блок внешних библиотек (flask, Django, и т.д.).
* Импорты из текущего проекта, не являющиеся относительными.

Каждый блок импортов должен быть отделен пустой строкой.

Пример:

    from __future__ import print_function

    import os
    import sys

    from flask import redirect
    import requests

    from yandex_directory.core.models.user import UserModel
    from yandex_directory.core.models.group import GroupModel

#### Импорт нескольких элементов

Если импортируется больше одного элемента модуля, то необходимо оформить их
в развернутом виде:

Да:

    from .models import (
        TestModel,
        NewModel,
        AnotherModelStill,
    )

Нет:

    from .models import TestModel, NewModel, AnotherModelStill

Нет:

    from .models import TestModel
    from .models import NewModel
    from .models import AnotherModelStill


### Базы данных

В этом разделе находится вся необходимая информацию для работы с БД в Яндекс.Директории.

#### Общая информацию

Мы используем [почтовый postgres](https://beta.wiki.yandex-team.ru/mail/pg/).

Мы не используем ORM и пишем чистый SQL. Конечно у нас есть сахар в виде [моделей](#modeli),
однако такие модели являются лишь тонкой абстракцией.

#### Шардирование

Почтовый постгрес предлагает [шардирование из коробки](https://beta.wiki.yandex-team.ru/mail/pg/queries/),
однако у этой реализации есть один большой недостаток - все запросы нужно оборачивать в хранимые процедуры.

Для шардирования на уровне приложения есть интересный инструмент - [sharpei](https://github.yandex-team.ru/mail/sharpei).
Sharpei представляет из себя бэкэнд с HTTP интерфейсом, который умеет отвечать на вопросы типа
"дай мне мастера из шарда, в котором находятся данные по такому UID". Нам это не подходит, т.к. шардируемся мы по
идентификатору организации.

Мы реализовываем работу с БД и шардами на уровне приложения

#### Структура шарда

Каждый шард состоит из одной мастер БД и двух реплик. Одна из реплик синхронная.
В случае отключения мастера синхронная реплика занимает его место и становится мастером. На данный момент переключение
делается вручную админами.

#### Адреса хостов

Хосты с шардами забираются из [кондуктора](https://c.yandex-team.ru/) по
[API](https://c.yandex-team.ru/api-cached/groups2hosts/mail_pg_common_test/?format=json).
Например, если запросить список хостов в группе `mail_pg_common_test`, то мы получим следующий список хостов:

    pg-common-test01d.cmail.yandex.net
    pg-common-test01e.cmail.yandex.net
    pg-common-test01h.cmail.yandex.net
    pg-common-test02d.cmail.yandex.net
    pg-common-test02e.cmail.yandex.net
    pg-common-test02h.cmail.yandex.net

Номер шарда зашит в названии хоста. В первом шарде находятся хосты:

* pg-common-test0**1**d.cmail.yandex.net
* pg-common-test0**1**e.cmail.yandex.net
* pg-common-test0**1**h.cmail.yandex.net

Во втором шарде находятся хосты:

* pg-common-test0**2**d.cmail.yandex.net
* pg-common-test0**2**e.cmail.yandex.net
* pg-common-test0**2**h.cmail.yandex.net

Если в названии хоста не присутствует цифра, по которой можно идентифицировать шард, или значение хоста равно `127.0.0.1`,
то мы считаем, что хост относится к первому шарду.

#### Роль хоста

БД на хосте может иметь роль мастера или реплики. Для определения роли базы можно выполнить запрос вида:

    show transaction_read_only;

Если ответ `on` - мы на реплике, если `off` - на мастере.

Для определения роли хоста можно воспользоваться функцией `get_database_role`
из модуля `yandex_directory.common.db`:

    >>> from yandex_directory.common.db import (
    ...     get_database_role
    ... )

    >>> get_database_role(...)
    'master'

#### Список баз данных

Список всех используем баз данных указывается в настройках в виде словаря `DATABASES`.
Каждое значение элемента словаря должно представлять из себя словарь со следующими ключами:

* **host** - хост БД. Если указан, то используется как единственный хост текущей БД.
Если имеет значение `None`, то хосты достаются из кондукторной группы, указанной в ключе `conductor_group`
* **port** - порт, на котором слушает демон БД
* **database** - название базы данных
* **user** - логин пользователя базы данных
* **password** - пароль доступа к базе данных
* **connect_args** - словарь с дополнительными аргументами, которые будут использоваться при каждом соединении с БД
* **conductor_group** - название кондукторной группы, на [хостах](#adresa-hostov) которой расположены шарды БД

Пример настроек:

    DATABASES = {
        'main': {
            'host': None,
            'port': 6432,
            'database': 'dirdb',
            'user': 'ydir',
            'password': '123456',
            'conductor_group': 'mail_pg_common_test'
        },
        'meta': {
            'host': '127.0.0.1',
            'port': 5432,
            'database': 'meta_dirdb',
            'user': 'meta_ydir',
            'password': '654321'
        },
    }

#### Alias базы

Алиасом базы является ключ, под которым она указана в [списке баз данных](#spisok-baz-dannyih).
Например, у [главной базы](#glavnaya-baza) алиас `main`. У [метабазы](#metabaza) алиас `meta`.

#### Главная база

Главная база хранит всю основную информацию по организациям, отделам, пользователям и т.п. Имеет [алиас](#alias-bazyi) `main`.

[Здесь](https://beta.wiki.yandex-team.ru/mail/pg/dirdb/) можно посмотреть на админскую конфигурацию главной БД.

#### KPI для главной базы

Отказ мастера главной базы влечет за собой уход в read-only данных всех организаций, попавших в шард с этой БД.
При этом реплики должны полностью обеспечивать функционирование запросов на чтение.

#### Метабаза

Т.к. мы реализовываем шардирование на уровне приложения, то нам нужно хранить информацию, на каком из шардов
размещаются данные определенной организации. Для этого существует отдельнам метабаза. Имеет [алиас](#alias-bazyi) `meta`.

#### KPI для метабазы

На каждый запрос в API делается запрос в метабазу (для определения шарда организации). Отказ мастера
метабазы для нас не так критичен, т.к. в этом случае не будет работать создание новых организаций.
Однако полный отказ шарда метабазы при запросах на чтение приведет к недоступности всего сервиса.

#### Workflow работы с БД

Для менеджинга транзакций, пула запросов и соединений мы используем [SQLAlchemy](http://www.sqlalchemy.org/).
Более низкоуровневое описание работы с тразакциями и соединениями можно найти [здесь](http://docs.sqlalchemy.org/en/latest/core/connections.html).
Про пулы соединений можно почитать [здесь](http://docs.sqlalchemy.org/en/latest/core/pooling.html).

Точкой входа при работе с БД являются так называемые [engines](http://docs.sqlalchemy.org/en/latest/core/connections.html#connection-engine-api).

Мы используем уровень изоляций транзакций `read committed`.

##### Engines

Каждый отдельный engine инкапсулирует в себе:

* Пул соединений с одной БД
* API для забора/отпускания соединений из пула

При старте приложения на [каждый из хостов](#adresa-hostov) создается по engine в глобальном словаре `engines`
, который находится в модуле `yandex_directory.common.db`.
Словарь `engines` имеет сложную структуру, которая позволяет эффективно запрашивать соединения к мастер
базам и репликам нужного шарда. Листьями являются объекты типа
[Engine](http://docs.sqlalchemy.org/en/latest/core/connections.html#connection-engine-api):

    {
        'meta': {
            1: {
                'master': [engine],
                'replica': [engine, engine],
            },
        }
        'main': {
            1: {
                'master': [engine],
                'replica': [engine, engine],
            },
            2: {
                'master': [engine],
                'replica': [engine, engine],
            }
        }
    }

На первом уровне alias базы, на втором шард, на третьем тип базы master
или реплика, а затем список пулов коннектов.

У каждого `engine` есть атрибут `db_info` со словарём, откуда можно узнать
дополнительную информацию. Важнее всего там ключ `'is_alive'`.


##### Соединения с базами

В обычных ситуациях, вам не надо заботиться о том, чтобы получить коннект к базе.
Во вью, коннекты к мета и обычной базам передаются прямо в метод, в качестве двух
первых параметров, в management команда унаследованных от TransactionalCommand или
AllShardsCommand, а так же в тесткейсах, доступны атрибуты self.meta_connection и
self.main_connection.

Коннекты нужно передавать явно в модели и функции, внутри которых идёт обращение к базе.
Это упрощает отладку и всегда понятно где и когда был установлен коннект.

Если всё таки нужно установить коннект вручную, то для этого существует две функции:

Первая, `get_meta_connection`, устанавливает соединение с метабазой. Она может принимать
дополнительный аргумент `for_write=True` и тогда соединение будет установлено с мастер-базой.
По умолчанию, будет выбрана одна из реплик, а в случае недоступности реплик - мастер.

Вторая функция `get_main_connection`, принимает один обязательный параметр `shard` - номер
шарда, и всё тот же `for_write`.

Обе функции возвращают контекстные менеджеры, а не сами коннекты, поэтому использовать их надо
в блоке with:

```
with get_main_connection(shard) as main_connection:
    делаем что-то с базой
    а по завершении блока коннект вернётся в пул
```

##### Транзакционность

Если надо выполнить код в транзакции, то нужно вызвать у коннекта `begin_nested`, так же в блоке `with`:

```
with get_main_connection(shard) as main_connection, \
         main_connection.begin_nested():
    делаем что-то с базой
    а по завершении блока коннект вернётся в пул
```

Если код выполнится без исключений, транзакция закоммится, если нет, будет автоматический роллбэк.
Ничего руками менеджить не надо.

О транзакционности выполнения view и команд, унаследованных от `TransactionalCommand` да `AllShardsCommand`,
беспокоиться не нужно, там `begin_nested` делается автоматически.


##### Если всё же нужно пройтись по всем шардам

В редких исключениях (например когда нужно поискать организацию по домену во всех шардах),
нужно во вью или модели пройтись по всем шардам. Для этого, надо получить список с шардами
с помощью вспомогательной функции `get_shard_numbers`:

```
shards = get_shard_numbers()

for shard in shards:
    with get_main_connection(shard, for_write=True) as main_connection, \
             main_connection.begin_nested():
        делаем что-то
        и оно автоматически коммитится, если не было исключений
```

##### Консольный доступ к БД

Для быстрого консольного доступа к БД существует специальная консольная команда:

    $ python manage.py dbshell -d main

На вход команда принимает следующие аргументы:

* `-d` - [алиас](#alias-bazyi) базы
* `-r` - роль базы
* `-s` - номер шарда
* `-h` - название хоста
* `-i` - информация по хостам. В случае указания этого аргумента соединение с БД не будет установлено

Например, соединиться с мастером метабазы:

    $ python manage.py dbshell -d meta -r master

Соединиться с репликой главной базы на втором шарде:

    $ python manage.py dbshell -d main -r replica -s 2

Показать все хосты главной базы:

    $ python manage.py dbshell -d main -i 1

    Shard 1
    pg-common-test01d.cmail.yandex.net
    pg-common-test01e.cmail.yandex.net
    pg-common-test01h.cmail.yandex.net

    Shard 2
    pg-common-test02d.cmail.yandex.net
    pg-common-test02e.cmail.yandex.net
    pg-common-test02h.cmail.yandex.net

Соединиться с определенным хостом главной базы:

    $ python manage.py dbshell -d main -h pg-common-test02e.cmail.yandex.net

#### Failover

В Я.Директории реализован функционал автоматического переключения используемой конфигурации баз данных в случае возникновения
следующих ситуаций:

* Недоступность хоста с БД
* Переключение мастера БД с одного хоста на другой

При старте API приложение использует следующие конфигурационные файлы:

* `/var/lib/yandex/yandex-directory/<environment>/databases_hosts.json` - файл со списком [хостов](#adresa-hostov), на
которых находятся базы данных.
* `/var/lib/yandex/yandex-directory/<environment>/databases_info.json` - файл с информацией о
топологии баз данных (на каких шардах находятся, живы ли хосты, являются ли базы мастерами или репликами)

`<environment>` обозначает текущее окружение, из под которого запускается приложение. В случае отсутствия конфигурационных
файлов приложение гарантирует их создание при старте.

После старта приложения используемые конфигурации кэшируются и используются в качестве источников информации
для установки [соединений с базами](#soedineniya-s-bazami). Стоит обратить внимание, что в случае изменения
конфигурационных файлов приложение не будет в автоматическом режиме использовать новую конфигурацию. Для этого потребуется
рестарт воркеров.

#### Обновление конф. хостов

Для обновления конфигурации хостов (`databases_hosts.json`) можно воспользоваться командой `check-databases-hosts`:

    $ python manage.py check-databases-hosts

Данная команда добавлена в крон файл пакета директории и запускается раз в час.

#### Обновление инф. о базах

Для обновления информации о базах данных (`databases_info.json`) можно воспользоваться командой `check-databases-info`:

    $ python manage.py check-databases-info

Возможные аргументы:

* `-r` - выполнять ли graceful рестарт воркеров пакета `yandex-directory` в случае изменения конфигурации баз данных.
По умолчания рестарт не выполняется.
* `-i` - интервал повторения проверки и обновления конфигурации (в секундах).
По умолчания интервал равен нулю и проверка выполняется только 1 раз
* `-l` - время жизни всех проверок (в секундах). Актуально только в случае указания интервала проверок. По умолчанию равно 60с

Например, следующая команда будет в течение 10 секунд проверять обновление конфигурации баз данных. Каждая проверка будет
выполняться с интервалом 3 секунды. В случае наличия обновлений, оно будет сохранено в конфигурационный файл `databases_info.json`
и воркеры пакета `yandex-directory` будут рестартованы:

    $ python manage.py check-databases-info -l 10 -i 3 -r 1

При запуске команды создается локальный лок на выполнение команды на текущем хосте. Это означает, что в случае существующего
запущенного процесса обновления конфигурации баз данных невозможен запуск обновления в другом процессе:

    $ python manage.py check-databases-info

    Database info checking is already in progress in another process

Данная команда добавлена в крон файл пакета директории и запускается раз в минуту. При этом проверки
выполняются в течение 55 секунд каждую секунду. В случае наличия обновлений, воркеры пакета рестартуются.

### Модели

Модель не является типичным представление ORM класса. Модель - просто сахар над utils методами определенной сущности.
Манипулирование сущностями должно осуществляться с помощью простых питонячьих типов. Например:

    >>> UserModel(connection=conn).create(name='gena')

    {
        'name': 'gena',
        'id': 10,
    }

Как вы видите, метод `create` возвращает простой тип словаря, а не инстанс класса `UserModel`.
Тоже самое относится и к методам поиска сущностей:

    >>> UserModel(connection=conn).find({'department_id': 1})

    [
        {
            'name': ...,
            'id': ...,
        },
        {
            'name': ...,
            'id': ...,
        },
    ]

Опять же, метод возвращает простой тип списка словарей.

#### Базовый класс

Базовый класс модели находится в модуле `yandex_directory.common.models.base`:

    from yandex_directory.common.models.base import BaseModel

При создании наследника базового класса необходимо установить:

* **table** - название таблицы в БД, с которой будем взаимодествовать модель
* **db_alias** - [алиас](#alias-bazyi) базы

Так же, можно указать порядок сортировки по-умолчанию:

* **order_by** - для большинства моделей подойдет просто `'id'`.
  Этот параметр не обязательный.


Пример:

    class UserModel(BaseModel):
        table = 'users'
        db_alias = 'main'
        order_by = 'id'

#### Используемое соединение

При инициализации инстанса модели можно напрямую передать соединение, которое должно использовать
при любой интерактивности данного инстанса с базой данных. Пример:


    from yandex_directory.common.db import get_connections

    connection = get_connections(
        db_alias='main',
        role='replica',
        shard=2,
    )[0]

    UserModel(connection=connection).find()

В описанном выше примере в первую реплику базы `main` из шарда `2` выполнится запрос на поиск всех сущностей пользователей.


Для получения соединения внутри модели нужно использовать метод `get_connection`. Этот метод принимает единственный атрибут `for_`, в который необходимо передать информацию о том, является ли запрос на чтение или на запись. Если запрос на запись, то значение атрибута `write`. Если запрос на чтение, то значение атрибута `read`.

Пример выполнения запроса на запись:

    class UserModel(BaseModel):
        ...

        def create(self, name):
            self.get_connection(for_="write").execute(...)

По умолчанию атрибут `for_` имеет значение `write`.

Метод `get_connection` выбирает соединение следующим образом.

Если инстанс модели был инициализирован с атрибутом `connection`, то вне зависимости от природы запроса (на чтение или запись) будет возвращено это соединение.

Если инстанс модели был инициализирован без атрибута `connection` и запрашивается соединение на запись (атрибут `for_` равен `write`):

* Если инстанс модели был инициализирован с атрибутом `connection_for_write`, то будет возвращено это соединение
* Иначе будет выполнена попытка использовать [рекумендуемое глобальное соединение](#rekomenduemyie-soedineniya) с базой для записи
* Если ни того, ни другого соединения не установлено, то возбуждается исключение

Если инстанс модели был инициализирован без атрибута `connection` и запрашивается соединение на чтение (атрибут `for_` равен `read`):

* Если инстанс модели был инициализирован с атрибутом `connection_for_read`, то будет возвращено это соединение
* Иначе будет выполнена попытка использовать [рекумендуемое глобальное соединение](#rekomenduemyie-soedineniya) с базой для чтения
* Если ни того, ни другого соединения не установлено, то выполняется попытка получить соединение с базой на запись, описанная выше

#### Выполнение запросов

Для выполнения запросов необходимо вызвать метод `execute` возвращаемого методом `get_connection` соединения:

    class UserModel(BaseModel):
        def create(self, name):
            self.get_connection(for_='write').execute(
                "INSERT INTO users (name) VALUES (%(name)s)",
                {
                    'name': 'gena'
                }
            )

Иногда необходимо преобразовать запрос сначала в строчку и только потом отправить его в базу данных. Для этого у
модели существует метод `mogrify`:

    class UserModel(BaseModel):
        def create(self, name):
            query = self.mogrify(
                "INSERT INTO users (name) VALUES (%(name)s)",
                {
                    'name': 'gena'
                }
            )
            self.get_connection(for_='write').execute(query)

Для получения данных выборки по одной сущности необходимо воспользоваться методом `fetchone`. Обратите внимание, что
возвращаемые объект является инстансом [RowProxy](http://docs.sqlalchemy.org/en/rel_0_9/core/connections.html#sqlalchemy.engine.RowProxy)
и его необходимо явно преобразовывать в словарь:

    class UserModel(BaseModel):
        def get(self, id):
            user = self.get_connection(for_='read').execute(
                "SELECT FROM users WHERE id = %(id)s LIMIT 1",
                {
                    'id': id
                }
            ).fetchone()
            return dict(user)

Для получения данных выборки по набору сущностей необходимо воспользоваться методом `fetchall`. Обратите внимание, что
возвращаемые объект является инстансом [ResultProxy](http://docs.sqlalchemy.org/en/rel_0_9/core/connections.html#sqlalchemy.engine.ResultProxy)
и его элементы необходимо явно преобразовывать в словарь:

    class UserModel(BaseModel):
        def find(self):
            users = self.get_connection(for_='read').execute(
                "SELECT FROM users"
            ).fetchall()
            return map(dict, users)

#### Возвращаемые значения

В случае, если метод модели возвращает данные из базы данных, то они должны быть явно преобразованы в простой словарь.

#### Поиск

Для поиска сущностей у модели определен метод `find`, который на вход принимает следующие атрибуты:

* **filter_data** - словарь, описывающий условия выборки.
Для корректной работы фильтрации ознакомьтесь с [соответствующим разделом](#filtryi).
* **skip** - какое количество сущностей нужно пропустить.
* **limit** - каким количеством сущностей нужно ограничить выборку.
* **select_related** - список связанных напрямую (через FK) сущностей,
которые нужно раскрыть при формировании ответа ([подробнее](#select-related)).
* **prefetch_related** - список связанных M2M сущностей,
которые нужно раскрыть при формировании ответа ([подробнее](#prefetch-related)).
* **order_by** - поля, по которым должна быть выполнена сортировка. Например: `'name, -id'`.

Пример выборки пользователей со вторым департаментом, пропуском первых 10, ограничением 100:

    >>> UserModel(connection=conn).find(
    ...     filter_data={'department_id': 2},
    ...     skip=10,
    ...     limit=100,
    ... )

    [
        {
            'name': ...,
            'id': ...,
            'department_id': 2
        },
        {
            'name': ...,
            'id': ...,
            'department_id': 2
        },
        ... список из 100 пользователей
    ]

Подробнее про раскрытие полей выборки во вложенные объекты можно почитать [здесь](#obektyi-iz-polej-vyiborki).

#### Количество сущностей

Для получения информации о количестве сущностей в БД можно воспользоваться методом `count`, который принимает следующие аргументы:

* **filter_data** - словарь, описывающий условия выборки.
Для корректной работы фильтрации ознакомьтесь с [соответствующим разделом](#filtryi).

#### Удаление сущностей

Для удаления сущностей в БД можно воспользоваться методом `delete`, который принимает следующие аргументы:

* **filter_data** - словарь, описывающий условия выборки.
Для корректной работы фильтрации ознакомьтесь с [соответствующим разделом](#filtryi).

#### Обновление сущностей

Для обновления сущностей в БД можно воспользоваться методом `update`, который принимает следующие аргументы:

* **update_data** - словарь с обновляемыми данными. В случае передачи пустого словаря будем возбуждено исключение.
* **filter_data** - словарь, описывающий условия выборки.
Для корректной работы фильтрации ознакомьтесь с [соответствующим разделом](#filtryi).

#### Выбор отдельной сущности

Для выбора отдельной сущности необходимо использовать метод `get`. Этот метод является абстрактным и требует
переопределения в конечных классах. Внутри себя этот метод может использовать [метод поиска](#poisk):

    class UserModel(BaseModel):
        ...

        def get(self,
                user_id,
                org_id,
                select_related=None,
                prefetch_related=None):
            response = self.find(
                filter_data={
                    'id': user_id,
                    'org_id': org_id
                },
                select_related=select_related,
                prefetch_related=prefetch_related,
                limit=1
            )

            if response:
                return response[0]

Обратите внимание, что желательно не забывать прокидывать [select\_related](#select-related) и
[prefetch\_related](#prefetch-related) атрибуты в метод `find`, т.к. может понадобиться раскрывать вложенные сущности и в
методе `get`.

Зачем нужен метод `get`, если есть метод `find`? Дело в том, что метод `get` может жестко определить интерфейс,
необходимый для выборки определенной сущности модели. В данном случае обязательным является указание идентификатора
пользователя (`user_id`) и идентификатора организации (`org_id`), в которую он входит.

#### Обновление опр. сущности

Для обновления отдельной сущности необходимо использовать метод `update_one`. Этот метод является абстрактным и требует
переопределения в конечных классах. Внутри себя этот метод может использовать [метод update](#obnovlenie-suschnostej):

    class UserModel(BaseModel):
        ...

        def update_one(self,
                       user_id,
                       org_id):
            if data:
                self.update(
                    update_data=data,
                    filter_data={
                        'id': id,
                        'org_id': org_id,
                    }
                )

            send_notification_about_user_changes()

Зачем нужен метод `update_one`, если есть метод `update`? Дело в том, что метод `update_one` может жестко определить интерфейс,
необходимый для выборки определенной сущности модели. В данном случае обязательным является указание идентификатора
пользователя (`user_id`) и идентификатора организации (`org_id`), в которую он входит.

В дополнении разработчик может прописать какие-нибудь постобработчики внутри метода обновления определенной сущности. Например,
в данном случае после обновления пользователя вызывается функция для нотификации о выполненном действии.

#### Удаление опр. сущности

Для удаления отдельной сущности необходимо использовать метод `delete_one`. Этот метод является абстрактным и требует
переопределения в конечных классах. Внутри себя этот метод может использовать [метод delete](#udalenie-suschnostej):

    class UserModel(BaseModel):
        ...

        def update_one(self,
                       user_id,
                       org_id):
            if data:
                self.delete_one(
                    filter_data={
                        'id': id,
                        'org_id': org_id,
                    }
                )

            send_notification_about_user_deleted()

Зачем нужен метод `delete_one`, если есть метод `delete`? Дело в том, что метод `delete_one` может жестко определить интерфейс,
необходимый для удаления определенной сущности модели. В данном случае обязательным является указание идентификатора
пользователя (`user_id`) и идентификатора организации (`org_id`), в которую он входит.

В дополнении разработчик может прописать какие-нибудь постобработчики внутри метода удаления определенной сущности. Например,
в данном случае после удаления пользователя вызывается функция для нотификации о выполненном действии.

#### Создание сущности

Для создания отдельной сущности необходимо использовать метод `create`. Этот метод является абстрактным и требует
переопределения в конечных классах.

    class UserModel(BaseModel):
        ...

        def create(self,
                   id,
                   org_id
                   name):
            self.get_connection(for_='write').execute('INSERT ...')

#### Фильтры

По умолчанию модель не умеет выполнять фильтрацию по переданным параметрам `filter_data`. Например:

    >>> UserModel(connection=conn).find({'group_id': 1})

    ValueError: There is no filter for "group_id" specified

    >>> UserModel(connection=conn).count({'group_id': 1})

    ValueError: There is no filter for "group_id" specified

Для работы фильтрации необходимо переопределить метод `get_filters_data`, который на вход принимает следующие параметры:

* **filter_data** - словарь, описывающий условия фильтрации.

Метод `get_filters_data` должен возвращать tuple, состоящий из трех списков.

Первый список содержет условия. Например:

    [
        'id = 1',
        'department_id IN (1,2,3)'
    ]

Второй список содержет джоины. Например:

    [
        '''
        LEFT OUTER JOIN user_group_membership as membership ON (
            users.org_id = membership.org_id AND
            users.id = membership.user_id
        )
        ''',
        '''
        LEFT OUTER JOIN resource_relations ON (
            users.org_id = resource_relations.org_id
        )
        '''
    ]

Третий список содержет все ключи из `filters_data`, которые учавствовали в формировании условий:

    [
        'id,
        'department_id'
    ]

Именно по этому списку происходит идентификация наличия фильтров, которые никак не повлияют на выборку. В случае наличия
таких фильтров будет возбуждено исключение.

Пример реализации метода `get_filters_data` с добавлением фильтрации по `group_id`:

    class UserModel(BaseModel):
        ...

        def get_filters_data(self, filter_data):
            if not filter_data:
                return [], [], []

            filter_parts = []
            joins = []
            used_filters = []

            if 'group_id' in filter_data:
                # добавляем условие
                filter_parts.append(
                    self.mogrify(
                        'membership.group_id = %(group_id)s',
                        {
                            'group_id': filter_data.get('group_id')
                        }
                    )
                )
                # добавляем джоин
                joins.append("""
                LEFT OUTER JOIN user_group_membership as membership ON (
                    users.org_id = membership.org_id AND
                    users.id = membership.user_id
                )
                """)
                # добавляем в использованные фильтры
                used_filters.append('group_id')

            return filter_parts, joins, used_filters

#### Объекты из полей выборки

SQL предполагает возврат plain списка на каждый столбец выборки.

Например:

    SELECT users.name, department FROM users
    LEFT OUTER JOIN departments as department ON (
        users.department_id = department.id
    )

Результат:

    [
        {
            'name': 'Гена',
            'department': '(333,1)'
        }
    ]

Однако хотелось бы получить каждую отдельную сущность как объект.
Функция `covert_keys_with_dots_to_items`, находящаяся в модуле `yandex_directory.common.utils`,
умеет раскрывать ключи с точками в самостоятельные объекты. Например:

    SELECT users.name,
           department
           department.id as "department.id",
           department.parent_id as "department.parent_id"
    FROM users
    LEFT OUTER JOIN departments as department ON (
        users.department_id = department.id
    )

Из базы будет возвращен ответ типа:

    [
        {
            'name': 'Гена',
            'department': '(333,1)',
            'department.id': 333,
            'department.parent_id': 1,
        }
    ]

Результат использования функции `covert_keys_with_dots_to_items`:

    >>> from yandex_directory.common.utils import (
    ...    covert_keys_with_dots_to_items
    ... )

    >>> covert_keys_with_dots_to_items(
    ...     {
    ...         'name': 'Гена',
    ...         'department': '(333,1)',
    ...         'department.id': 333,
    ...         'department.parent_id': 1,
    ...     }
    ... )

    {
        'name': 'Гена',
        'department': {
            'id': 333,
            'parent_id': 1
        }
    }

Обратите внимание, что обязательно указание корневого элемента `department`. В случае, если он не будет указан,
вложенные объекты не будут формироваться:

    >>> covert_keys_with_dots_to_items(
    ...     {
    ...         'name': 'Гена',
    ...         'department.id': 333,
    ...         'department.parent_id': 1,
    ...     }
    ... )

    {
        'name': 'Гена'
    }

Если корневой элемент равен `None`, то раскрытие объекта тоже не происходит:

    >>> covert_keys_with_dots_to_items(
    ...     {
    ...         'name': 'Гена',
    ...         'department': None,
    ...         'department.id': 333,
    ...         'department.parent_id': 1,
    ...     }
    ... )

    {
        'name': 'Гена',
        'department': None
    }

#### Select related

При выборке сущностей возможно указание списока связанных напрямую (через FK) сущностей,
которые нужно раскрыть при формировании ответа.
Аналогично джанговскому [select_related](https://docs.djangoproject.com/en/1.8/ref/models/querysets/#select-related).

Например, у пользователя есть связанный с ним через foreign key `department_id` департамент:

    >>> UserModel(connection=conn).get(id=1, org_id=1)

    {
        id: 1,
        department_id: 100,
        ...
    }

Чтобы автоматически заменить идентификатор департамента на связный объект, этот объект нужно указать в списке `select_related`:

    >>> UserModel(connection=conn).get(
    ...     id=1,
    ...     org_id=1,
    ...     select_related=['department'],
    ... )

    {
        id: 1,
        department: {
            id: 100,
            name: ...
        },
        ...
    }

Для работы `select_related` необходимо переопределить метод `get_select_related_data`, который на вход принимает следующие параметры:

* **select_related** - список объектов для раскрытия

Метод `get_select_related_data` должен возвращать tuple, состоящий из двух списков.

Первый список содержет поля выборки. Например:

    [
        'users.*',
        'department',
        'department.id AS "department.id"',
    ]

Второй список содержет джоины. Например:

    [
        '''
        LEFT OUTER JOIN departments as department ON (
            users.department_id = department.id AND users.org_id = department.org_id
        )
        ''',
        '''
        LEFT OUTER JOIN departments as department_parent ON (
            department.parent_id = department_parent.id AND department.org_id = department_parent.org_id
        )
        '''
    ]

Пример реализации `select_related` для выборки департамента для каждой сущности пользователя:

    def get_select_related_data(self, select_related):
        if not select_related:
            return [self.default_all_projection], []

        select_related = select_related or []
        projections = []
        joins = []

        if 'department' in select_related:
            projections += [
                'users.*',
                'department',
                'department.id AS "department.id"',
                'department.name AS "department.name"',

                'department_parent AS "department.parent"',
                'department_parent.id AS "department.parent.id"',
                'department_parent.name AS "department.parent.name"',
                'department_parent.parent_id AS "department.parent.parent_id"',
            ]
            joins.append("""
            LEFT OUTER JOIN departments as department ON (
                users.department_id = department.id AND users.org_id = department.org_id
            )
            LEFT OUTER JOIN departments as department_parent ON (
                department.parent_id = department_parent.id AND department.org_id = department_parent.org_id
            )
            """)

        return projections, joins

Подробнее про раскрытие полей выборки во вложенные объекты можно почитать [здесь](#obektyi-iz-polej-vyiborki).

#### Prefetch related

Список связанных M2M сущностей, которые нужно раскрыть при формировании ответа выборки.
Аналогично джанговскому [prefetch_related](https://docs.djangoproject.com/en/1.8/ref/models/querysets/#prefetch-related).

Например, у пользователя есть связанные с ним через промежуточную таблицу группы:

    >>> UserModel(connection=conn).get(id=1, org_id=1)

    {
        id: 1,
        group_ids: [
            1,
            2,
            3
        ],
        ...
    }

Чтобы автоматически заменить идентификаторы групп на связный объект, этот объект нужно указать в списке `prefetch_related`:

    >>> UserModel(connection=conn).get(
    ...     id=1,
    ...     org_id=1,
    ...     prefetch_related=['groups'],
    ... )

    {
        id: 1,
        groups: [
            {
                id: 1,
                name: ...
            },
            {
                id: 2,
                name: ...
            },
            {
                id: 3,
                name: ...
            },
        ]
        ...
    }

Для работы `prefetch_related` необходимо переопределить метод `prefetch_related`, который на вход принимает следующие параметры:

* **items** - список объектов текущей сущности, для которых нужно произвести раскрытие связанных сущностей
* **prefetch_related** - список объектов для раскрытия

Метод `prefetch_related` не должен ничего возвращать. Его главная задача - модификация `items` с добавлением
связанных с ним M2M связью сущностей.

Пример реализации раскрытия групп пользователей:

    def prefetch_related(self, items, prefetch_related):
        if not prefetch_related or not items:
            return

        if 'groups' in prefetch_related:
            user_groups = {}
            for group in GroupModel().find(filter_data={
                'user_id__in': [i['id'] for i in items]
            }):
                user_groups.setdefault(group['user_id'], []).append(group)

            for user in items:
                user['groups'] = user_groups.get(user['id'], [])

### Миграции

Всей файлы с миграциями находятся в директории `src/yandex_directory/core/db/migrations/`.
Для [главной базы](#glavnaya-baza) миграции находятся в поддиректории `main/migrations`.
Для [метабазы](#metabaza) миграции находятся в поддиректории `meta/migrations`.
Надо не забыть добавить в миграцию для [главной базы](#glavnaya-baza) выдачу прав, если добавляются новые таблицы.
`GRANT ALL ON ALL TABLES IN SCHEMA ydir TO ydir;`
`GRANT ALL ON ALL SEQUENCES IN SCHEMA ydir TO ydir;`

#### Именование файлов миграций

Файл с названием миграции должен начинаться с буквы `V` и порядковым номером миграции. Номер миграции должен состоять
минимум из 4 цифр. Например, номер первой миграции `0001`, номер второй `0002` и т.д. Далее через двойное подчеркивание
`__` должено следовать краткое описание миграции. Если миграцию нельзя или не нужно заворачивать в транзакцию (а это по умолчанию делается), то краткое описание должно начинаться со слова `NONTRANSACTIONAL`. Заканчиваться название файла должно расширением `.sql`. Примеры:

* `V0001__initial_migration.sql`
* `V0002__NONTRANSACTIONAL_add_index_to_users.sql`

#### Как выкатывать миграции

Выкатка новых миграций происходит вручную. Команда `manage migrate` запустит все имеющиеся в коде миграции последовательно.

Писать миграции необходимо:
1. *максимально атомарно* (то есть так, чтобы накатка и откатка миграции имели минимум шансов сломаться "посередине")
2. *минимально блокирующе* (то есть так, чтобы с базой можно было работать, пока миграция бежит)

В идеале код нужно структурировать так, чтобы новый код работал и со смигрированными, и с несмигрированными данными. Это требование обусловлено тем, что наша база шардирована, и ситуаций, когда один шард смигрировал, а другой не смог, и из-за этого система работает только наполовину, иметь не хочется.

**Если в пулл-реквесте есть миграции, его название обязательно должно оканчиваться на `[MIGRATE]`.**

##### Style guide от админов:
* Длина строки < 80 символов
* Все новые строки внутри одного подзапроса делай с отступами от начала строки, на 4 пробела.
    CREATE TABLE ydir.organizations (
        id BIGINT NOT NULL,
        label TEXT NOT NULL,
        name JSONB NOT NULL,

        CONSTRAINT pk_organizations PRIMARY KEY (id)
    );
* Не пиши commit message на русском.

#### Именование индексов

Каждый отдельный тип индексов должен начинаться с определенного префикса. Обычный индекс должен использовать префикс `i_`. Далее должно следовать название таблицы, для которой этот индекс создается и поле, к для которого индекс строится. Пример:

    CREATE TABLE users (
        id INT,
        name TEXT
    );

    CREATE INDEX i_users_name ON users (name);


#### Составной индекс

При формирование составного индекса его именование должно придерживаться правил именования обычного индекса. Единственное отличие, что должны быть перечислены все поля в порядке их использования в индексе:

    CREATE TABLE users (
        id INT,
        name TEXT,
        surname TEXT
    );

    CREATE INDEX i_users_name_surname
        ON users (name, surname);

#### Первичный ключ

Constraint первичного ключа должен задаваться отдельно от объявления поля и именоваться с
префиксом `pk_`. За префиксом должно следовать название таблицы:

    CREATE TABLE organizations (
        id INT,
        CONSTRAINT pk_organizations PRIMARY KEY (id)
    );

Обратите внимание, что даже в случае если первичный ключ является составным, то его именование должно строго подчинаться алгоритму использования префикса + названия таблицы.

    CREATE TABLE groups (
        id INT,
        org_id INT,
        CONSTRAINT pk_groups PRIMARY KEY (org_id, id)
    );

#### Внешний ключ

При формирование внешнего ключа его название должно начинаться на префикс `fk_`:

    CREATE TABLE users (
        id BIGINT NOT NULL,
        org_id INT NOT NULL,
        department_id INT,

        CONSTRAINT id PRIMARY KEY,
        CONSTRAINT fk_users_org_id_department_id
            FOREIGN KEY (org_id, department_id)
            REFERENCES departments (org_id, id)
            ON DELETE CASCADE
    );

#### Индекс уникальности

Название индекса уникальности должно начинаться с префикса `uk_`:

    CREATE TABLE ydir.organizations (
        id INT,
        label TEXT NOT NULL,

        CONSTRAINT pk_organizations PRIMARY KEY (id)
    );

    CREATE UNIQUE INDEX uk_organizations_label ON organizations (label);

Обратите внимение на конструкцию `UNIQUE INDEX`. Если не указать инструкцию `INDEX`, то постгрес не создаст индекс и каждая проверка на уникальность по ключу будет использовать full scan.

#### ID организации в индексах

В нашей базе 99% запросов используют идентификатор организации как один из параметров выборки (поиск данных внутри определенной организации). В случае наличия идентификатора организации в составном индексе необходимо устанавливать его первым. Таким образом корень дерева индекса всегда будет начинаться с первичного ключа организации и процесс выборки будет более оптимальным. В примере ниже как первичный ключ, так и FK являются составными:

    CREATE TABLE ydir.departments (
        id INT,
        org_id INT,
        parent_id INT,

        CONSTRAINT pk_departments PRIMARY KEY (org_id, id),
        CONSTRAINT fk_departments_org_id_parent_id
            FOREIGN KEY (org_id, parent_id)
            REFERENCES departments (org_id, id)
    );

### Тестирование

В этом разделе описывается процесс написания тестов различного рода тестов при разработке проекта.

#### Структура тестов

О структуре тестов можно почитать [здесь](https://github.yandex-team.ru/pages/yandex-events/yandex-tech-api-docs/docs_dev.html#struktura-testov)

#### Запуск тестов

Для запуска тестов мы используем [tox](https://tox.readthedocs.org/en/latest/):

    $ pip install tox
    $ tox

Кастомные атрибуты тестов:

    $ tox -- --verbosity=3

Запуск тестов в определенном модуле:

    $ tox -- tests.unit.yandex_directory.core

Запуск тестов определенного TestCase:

    $ tox -- tests.unit.yandex_directory.core.models.user.tests:UserModelTest

#### Smoke тесты

Данный тип тестов используется при деплое и показывает, есть ли необходимые приложению дырки и гранты.

    $ cd src/
    $ python manage.py smoke-test

При добавления взаимодействия с каким-либо удаленным бэкэндом необходимо добавлять и smoke тесты,
проверающие доступность этого бэкэнда. Примеры:

* Соединение с postgres базами
* Дырки до паспорта
* Гранты для паспорта
* SMTP соединение
* Соединение с PDD API


### Разработка

Общие сведения по разработке.

#### Создание организации

Для создания новой организации можно воспользоваться функцией `create_organization` из модуля
`yandex_directory.core.utils`:

    from yandex_directory.core.utils import create_organization

    create_organization(
        name={
            'ru': 'Яндекс',
            'en': 'Yandex'
        },
        label='yandex'
        author_id=321,
    )

Описанная выше функция выберет [наиболее подходящий](#vyibor-sharda) для новой организации шард и создаст все необходимые сущности в БД
из выбранного шарда.

#### Выбор шарда

Шард с минимальным количеством пользователей на момент создания новой организации будет выбран в качестве шарда для
этой организации.

### Определения

В этом разделе перечислены различные определения общего характера.

#### DSN

Пример:

    >>> from yandex_directory.common.utils import build_dsn
    >>> build_dsn(
    ...     host='127.0.0.1',
    ...     port=5432,
    ...     database='ydir',
    ...     user='web-chib',
    ...     password='12345',
    ... )
    'postgresql://web-chib:12345@127.0.0.1:5432/ydir'

#### Безопасный DSN

Является обычным DSN без указания логина и пароля. Может свободно фигурировать в логах.

Пример:

    >>> from yandex_directory.common.utils import build_dsn
    >>> build_dsn(
    ...     host='127.0.0.1',
    ...     port=5432,
    ...     database='ydir',
    ... )
    'postgresql://127.0.0.1:5432/ydir'

### Действия и события: Сохранении истории в базу, ревизия организации,
подписка

#### Действия
Действия, произведенный пользователем записываем в таблицу истории actions.
По этой таблице можно понять кто когда выполнил какое действие, составить аудит-лог,
а также найти все изменения от любой версии до текущей.
С появлением таблицы истории у нас появляется понятие ревизии организации.
Это целочисленный счетчик, единый на всю организацию. При каждом действии
значение счетчика инкрементируется.
Действие сохраняется в виде записи с полями:

* **org_id** - идентификатор организации
* **revision** - номер ревиции, единый на организацию
* **name** - название действия
* **author_id** - uid автора действия
* **object** - `JSON` объекта, который был изменён, уже в измененном состоянии
* **object_type** - тип объекта. Можно понять по названию события, например, `user_add`, относится в типу `user`.
Отдельное поле добавлено для быстрых выборок в базе. Поле может принимать следующие значения:
    * `user`
    * `department`
    * `group`
    * `resource`
* **old_object** - `JSON` представление объекта до изменений. Может быть пустым объектом для действий добавления и пр.
* **timestamp** - дата действия

Названия действий соотсветвует шаблону:
<object_type>_<action_type>, где
    object_type - один из типов ['user', 'department', 'group', 'resource'],
    action_type - глагол в настоящем времени (напр. 'add', 'modify', 'delete')

##### Список возможных действий
* **organization\_add** - добавление организаци
* **user\_add** - добавление нового сотрудника
* **user\_modify**  - изменение сотрудника (информация и перемещение)
* **department\_add** - добавление нового департамента
* **department\_modify**  - изменение департамента (информация и перемещение)
* **group\_add**  - добавление группы
* **group\_modify**  - изменение группы или состава группы
* **group\_delete**  - удаление группы
* **security\_user\_password_changed**  - смена пароля пользователю
* **security\_user\_blocked**  - пользователь заблокирован
* **security\_user\_unblocked**  - пользователь разблокирован
* **security\_user\_grant\_organization\_admin** - присвоение прав администратора организации
* **security\_user\_revoke\_organization\_admin** - лишение прав администратора организации


Планируем также поддержать:
* **organization\_modify** - изменение организаци
* **resource\_add** - добавление нового ресурса
* **relation\_modify** - сервис изменил права на ресурс
* сотрудник уволен
* сотрудник заблокирован


#### Сохранение действий

Действия вызываются из методов API, например, при POST /users/ вызывается
действие с названием 'user_add'.
Все действия вызываются через функции, которые начинаются с префикса action_.
Например: для действия с названием 'user_add' вызывается функция
'action_user_add'.:
Это соглашение для будущих действий, пока что оно не является правилом
Запуск событий из действий происходит через функцию event_generator, которая вызывает функции, совпадающие с суффиксом '<object_type>_<action_type>' и начинающихся с префикса 'on_'

Код для сохрания и обработки действий и событий находится
в папках `src/yandex_directory/core/actions` и `src/yandex_directory/core/events`

#### События и уведомления

Иногда клиенты хотят получать уведомления о некоторых изменениях. При этом
уведомлений только на действия пользователя не достаточно.
Например, при перемещении сотрудника в другой отдел,
чатик хочет получить уведомление про изменение состава чата,
а не про изменение состава департамента, про структуру компании чатик
 ничего не знает. Такие требования привели нас к идее событий.

  Действия (которые хранятся в actions) порождают цепочку событий(events).
  Клиент подписывается на нужные события и получает уведомления когда оно произошло.
  Цепочка порождения событий описана в клиентской документации
  https://api-internal-test.directory.ws.yandex.net/docs/index.html#tsepochka-porozhdeniya-sobyitij

События хранятся в таблице events в формате:

* **org_id** - идентификатор организации
* **revision** - номер ревиции, единый на организацию
* **name** - название действия
* **content** - дополнительные данные. Информация о предыдушем состоянии, признак косвенных измениний.
Представлено в виде `json`
* **object_type** - тип объекта. Можно понять по названию события, например, `user_add`, относится в типу `user`.
Отдельное поле добавлено для быстрых выборок в базе. Поле может принимать следующие значения:
    * `user`
    * `department`
    * `group`
    * `resource`
* **object** - объект, к которому относится событие. Представлено в виде `json`
* **timestamp** - дата события

Подробнее в описании класса event в src/yandex_directory/core/events.__init__.py

#### Подписка

На любое событие можно подписаться и получить данные когда оно произойдёт.
Интерфейс подписки пока не реализован. Сейчас для добавления подписки в
`settings.py` в `SUBSCRIPTIONS` надо прописать:

* URL колбэка и аутентификационный заголовок, если нужен
* Заголовки колбэка
* Название сервиса

Нотификации отправляются по `HTTP` посредством `POST` запроса на указанный `URL`.
Отправка сообщений происходит ассинхронно, с использованием очереди
python-rq и локального redis-а как брокера задач. При временном выключении
машины все уведомления будут разосланы когда машина вернется в рабочее
состояние.



### Определения

В этом разделе перечислены различные определения общего характера.

#### DSN

Пример:

    >>> from yandex_directory.common.utils import build_dsn
    >>> build_dsn(
    ...     host='127.0.0.1',
    ...     port=5432,
    ...     database='ydir',
    ...     user='web-chib',
    ...     password='12345',
    ... )
    'postgresql://web-chib:12345@127.0.0.1:5432/ydir'

#### Безопасный DSN

Является обычным DSN без указания логина и пароля. Может свободно фигурировать в логах.

Пример:

    >>> from yandex_directory.common.utils import build_dsn
    >>> build_dsn(
    ...     host='127.0.0.1',
    ...     port=5432,
    ...     database='ydir',
    ... )
    'postgresql://127.0.0.1:5432/ydir'

### Сборка пакета
Для сборки и выкатки в тестинг пакета запустите скрипт deploy.sh из
ветки master рабочей копии сновного репозитория.
- Комитит изменения версии, проставит в git tag с номером версии,
например v0.9.1
- Клонирует ветку мастер в ~/tmp/build и оттуда собирает пакет
- Заливает собранные пакет в репозиторий, для нас yandex-trusty
- Ставит в кондуктор тикет на выкатку в тестинг - нужен файл в ~/.conductor_auth с вашей аутентификационная кукой кондуктора. Добавляем ip машины откуда собираем в ACL в настройках конуктора. https://c
.yandex-team.ru/settings
