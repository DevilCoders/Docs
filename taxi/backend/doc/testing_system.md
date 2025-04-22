# Testing system

Content:

*   [Intro][toc-intro]
*   [Run tests][toc-run]
*   [Work with database][toc-db]
*   [Directory structure and naming conventions][toc-dir]
*   [Testing timeouts and freezing time][toc-sleep]
*   [Stubs, mocks and mocklevels][toc-mock]


## Intro

Our testing system is based on [pytest][pytest] with
[pytest-twisted][pytest-twisted] plugin. For details on used fixtures
and markers see `tests-pytest/conftest.py` and `tests-pytest/pytest.ini`
files.

There are conventions for naming test files and data for tests. See
[directory structure and naming conventions][toc-dir] for details.

[pytest][pytest] namespace is extended with `inline_callbacks` (provided
by `conftest.py`) and `inlineCallbacks` (provided by
[pytest-twisted][pytest-twisted] plugin) wrappers to write tests with
inline callbacks:

```python
@pytest.inline_callbacks
def test_something():
    doc = yield db.users.find_one({'_id': 'notexistent'})
    assert doc is None
```

By default test is executed two times: in blocking and asynchronous
environment. To run test only in one environment use `asyncenv` marker:

```python
@pytest.mark.asyncenv('blocking')
def test_something():
    ...
```

Control filling database with `filldb` marker. It is the only way to
prepare database for a test. See [Work with database][toc-db]
for details.

Test timeouts and frozen moments of time with `sleep` fixture and `now`
marker. See [Testing timeouts and freezing time][toc-sleep] for details.

Mock functions with `mock` fixture. Specify mock level with `mocklevel`
marker. Use `stub` fixture to replace objects. Generate (some) responses
with `response` fixture. See [Stubs, mocks and mocklevels][toc-mock] for
details.

Load static with `load` fixture. See
[Directory structure and naming conventions][toc-dir] for details.


## Run tests

Install all taxi runtime dependencies:

    sudo apt-get install -yy \
        memcached
        python
        python-celery
        ...

Install pytest with plugins and test dependencies:

    sudo pip install -i https://pypi.yandex-team.ru/simple/ pytest
    sudo pip install -i https://pypi.yandex-team.ru/simple/ pytest-twisted
    sudo pip install -i https://pypi.yandex-team.ru/simple/ pytest-timeout
    sudo pip install -i https://pypi.yandex-team.ru/simple/ freezegun

Run memcached and mongo:

    sudo service memcached start
    mkdir ~/mongodata
    cd ~/mongodata
    mkdir taxi1 taxi2 taxi3
    mongod --replSet taxi --port 11017 --dbpath ./taxi1 --logpath ./taxi1.log --pidfilepath ./taxi1.pid --fork
    mongod --replSet taxi --port 11018 --dbpath ./taxi2 --logpath ./taxi2.log --pidfilepath ./taxi2.pid --fork
    mongod --replSet taxi --port 11019 --dbpath ./taxi3 --logpath ./taxi3.log --pidfilepath ./taxi3.pid --fork
    python -c 'from pymongo import Connection;c=Connection("localhost:11017");print c.admin.command("replSetInitiate")'
    python -c 'from pymongo import Connection;c=Connection("localhost:11018");print c.admin.command("replSetInitiate")'
    python -c 'from pymongo import Connection;c=Connection("localhost:11019");print c.admin.command("replSetInitiate")'

Clone taxi repository:

    cd ~
    git clone git@github.yandex-team.ru:YOURLOGIN/backend.git taxi-backend

Run tests:

    cd taxi-backend/tests-pytest
    PYTHONPATH=.:..:$PYTHONPATH py.test tests-pytest/test_*.py

Note! It's possible `pytest_timeout` won't be imported. To fix it run
tests with `-p pytest_timeout` option:

    PYTHONPATH=.:..:$PYTHONPATH py.test -p pytest_timeout tests-pytest/test_*.py


## Work with database

*TODO: move dumping tools into taxi repository*

Dump database (most likely in production) with [tools][testing-tools]
which respect private and secure data. **Avoid to put sensetive data
(API keys, phones, names, passwords and so on) in repository**.

Put dump into test static directory. For example, dump of `users`
collection (let's dump banned users for example) for
`tests-pytest/test_something.py` file must be in
`tests-pytest/static/test_something/db_users_banned.json`.

Specify you want to use this dump in a test with `filldb` marker:

```python
@pytest.mark.filldb(users=banned)
def test_unban_users():
    ...
```

See [Directory structure and naming conventions][toc-dir] for details on
how and where to place files.


## Directory structure and naming conventions

Directory structure:

    tests-pytest/
        static/
            default/
                db_cities.json

            test_internal_users/
                db_users_banned.json
                somefile.xml

        test_core_async.py
        test_core_db.py
        ...

        test_external_router.py
        test_external_tracker.py
        ...

        test_internal_drivers.py
        test_internal_users.py
        ...

        test_client2x_auth.py
        test_client2x_order.py
        ...

        test_client30_auth.py
        test_client30_order.py
        ...

        test_taxi1x_carack.py
        test_taxi1x_requestconfirm.py
        ...

Load static files in a test:

```python
# somewhere in test_internal_users.py

def test_unban_users(load):
    binary = load('somefile.xml')
```


## Testing timeouts and freezing time

For freezing special moment of a time use `now` marker:

```python
@pytest.mark.now('2014-12-31 23:55:00 +03')
def test_president_speech():
    ...
```

For testing timeouts use `sleep` fixture along with `inlineCallbacks` or
`inline_callbacks` wrapper:

```python
@pytest.mark.asyncenv('async')
@pytest.inlineCallbacks
def test_something(sleep):
    # hack-hack-hack
    yield sleep(10)
    # Test what would happend in 10 seconds
```

If some i/o-blocking operations (actually, operations with database or
memcached) are run in another cycle of event loop wait for it
explicitly:

```
@pytest.inline_callbacks
def test_something(sleep):
    # For example, some document of `users` collection is updated in
    # a green thread with `call_later`, then
    yield some_operation_that_runs_call_later()
    yield sleep(0)
    yield db.users.find_one({'_id': 'someid'})

    # Or some key is set to memcached
    yield some_operation_that_runs_call_later()
    yield sleep(0)
    yield mc.get('key')
```


## Stubs, mocks and mocklevels

Usage of `stub` fixture:

```python
def test_something(stub):
    obj = stub(x=1, m=lambda y: y + 2)
    assert obj.x == 1
    assert obj.m(40) == 42
```

*TODO: describe mocking and mocklevels*


[pytest]: http://pytest.org
[pytest-twisted]: https://github.com/schmir/pytest-twisted
[testing-tools]: https://github.yandex-team.ru/dmkurilov/taxi-scripts/tree/master/tests

[toc-intro]: #intro
[toc-run]: #run-tests
[toc-db]: #work-with-database
[toc-dir]: #directory-structure-and-naming-conventions
[toc-sleep]: #testing-timeouts-and-freezing-time
[toc-mock]: #stubs-mocks-and-mocklevels
