Новая команда
=============

О чём необходимо помнить, когда добавляется новая команда.

Source
------

Код необходимо добавить в пакет `agency_rewards`.
Должна быть функция `main`, к которой потом необходимо привзять `entry_points` в
`setup.py` (см. далее).

Команда должна обязательно иметь флаг `--no-mnclose`, чтобы можно было запустить
без проверки состояния графа закрытия месяца.


setup.py
--------

Необходимо добавить путь к добавленному ранее коду в `entry_points`, чтобы в virtualenv
появилась cli-команда после `setup.py install`.

shell wrapper
-------------

Чтобы не забывать перед запуском команды активировать virtualenv или окружение для Oracle,
необходимо добавить shell обертку вида:

```bash
source /etc/yandex/yb-ar/env
exec /opt/venvs/yb-ar/bin/<имя-команды-из-setup.py> "$@"
```

Конфиги
-------

Как минимум, в конфиги необходимо добавить имя mclose задачи, которое необходимо проверять
перед запуском.
Пример:

```xml
     <MNClose>
         <Tasks>
            <Task id="import_domain_stats">ar_import_domain_stats</Task>
        </Tasks>
    </MNClose>
```

Где `id=import_domain_stats` - это то, что используется в исходном коде. А
`ar_import_domain_stats` - это реальное имя узла в графе закрытия mnclose.

А так же, необходимо помнить, что конфигов у нас несколько: по одному на каждую
среду (`dev, test, prod, local`). Значения необходимо добить во все.

Пример
======

- [yb-ar-import-domain-stat](https://github.yandex-team.ru/Billing/yb-ar/commit/d8782cfcd9e70db8b5872f5d36080aab7ea0f5e1)