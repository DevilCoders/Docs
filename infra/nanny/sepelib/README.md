This is SEPE commons library for python services, i.e. it's not a common library
for everyone. Just a bunch of utilities that are shared between services which
are gevent based daemons.

The library is split into a few packages grouped under one namespace package
named `sepelib`. The reason for that is to let people use some parts of it
without installing the whole large set of dependencies. Here is the list of
packages:

* `sepelib.gevent` — various helpers for gevent library;
* `sepelib.http` — http related utilities;
* `sepelib.mongo` — stuff related to MongoDB interactions;
* `sepelib.subprocess` — process management utilities;
* `sepelib.rpc` — remote procedure call utilities;
* `sepelib.util` — various helpers and utilities. Has no required dependencies
  at all and intended to stay that way;
* `sepelib.vcs` — utilities for working with version control systems;
* `sepelib.flask` — Flask-related stuff;
* `sepelib.yandex` — utilities for communicating with internal Yandex services;
* `sepelib.zookeeper` — stuff related to Zookeeper interactions.

Подробнее
=========

core
----

#### core.config

Модуль конфигурирования приложения. Пример:

    from sepelib.core import config
    # cfg_default.yml — Jinja2-шаблон YAML-конфига
    # config_context — данные для его рендеринга, считанные, например, из командной строки
    config.load('./cfg_default.yml', config_context={...})
    config.get_value('web.http.port')

#### core.constants

Константы навроде `MINUTE_SECONDS` или `NETWORK_TIMEOUT`.

#### core.exceptions

Два базовых класса для исключений: `Error` и `LogicalError`.

flask
-----

#### flask.auth

Реализует класс Authenticator — processor request для аутентификации пользователей через blackbox.
Предоставляет Mongoengine-модели для хранения списков доступов для пользователей и staff-групп.
Тесно завязан на Mongoengine и Flask-Principal.

#### flask.h

Множество мелких хелперов для чтения запросов и формирования ответов.

#### flask.server

HTTP-сервер со встроенными ручками /ping, /version, /config/, /reopen_log, /metrics, /yasm_stats.
Интегрирован с ``sepelib.metrics``.

gevent
------

`GreenThread` — thread-like обёртка над гринлетами.

http
----

Утилиты для взаимодействия с RESTful API через requests.
Реализует `InstrumentedSession` — подкласс `requests.Session`, провязанный с `sepelib.metrics`.

metrics
-------
Инструменты для подсчёта статистики — счетиков, перцентилей, средних значений и так далее.
Пример собранных данных: http://its.yandex-team.ru/metrics/?fmt=yaml

mongo
-----
Утилиты для работы с MongoDB через Mongoengine:

* недостающие поля: `EnumField`, `SetField`;
* поддержка недостающего `find_and_modify` в MongoEngine;
* метод `mock_database` — поднимает MongoDB и возвращает Mongoengine-connection к ней. Удобен для тестирования;
* классы для генерации последовательных идентификаторов моделей.

rpc
---
Утилиты для работы с Thrift и XML RPC.

#### rpc.xml

`xmlrpc_call` — функция-обёртка для вызова XML RPC методов, использует `requests` и `xmlrpclib`.

#### rpc.thrift

Реализует `ThriftHttpClient` и `ThriftBinClient`. Умеют восстанавливать соединение с сервером
прозрачно для пользователя, интегрированы с `sepelib.metrics`.

subprocess
----------

Функция terminate для правильной остановки процессов.

util
----
Множество маленьких функций — для форматирования исключений, работы с файловой системой, STMP, простые таймеры для профайлинга, декоратор для повторных попыток.

vcs
---

#### vcs.svnfile

Простой клиент для работы с SVN.

yandex
------
Клиенты к:

* alemate
* auth.qe.yandex-team.ru
* blackbox
* center-robot.yandex.net
* clustermaster
* CMS
* GenCfg
* ISS
* ITS
* Nanny
* oauth.yandex-team.ru
* OTRS
* passport
* Sandbox
* shardtracker.search.yandex.net
* Staff
* Startrek
* timeline.yandex-team.ru

zookeeper
---------
Клиент к Zookeeper и различные concurrency primitives поверх него:

* условные переменные (`Condition`, `ConditionListener`);
* локи (`Lock` — доработанная версия `kazoo.recipe.lock.Lock`, `InterruptableLock`), garbage collector для локов;
* `SingletonService` — реализует singleton green thread, координирующийся через Zookeeper;
* альтернативные реализации стандартных рецептов с более правильным API и поправленными багами;
* pytest fixture `zookeeper` — поднимает Zookeeper и предоставляет средства им управлять.

