###Питоновская обёртка над http-методами [mds](https://wiki.yandex-team.ru/mds/dev/protocol/)

#### Yandex pypi
https://pypi.yandex-team.ru/packages/mdswrapper/

#### Для разработки
Нужно положить в tests/local_settings.py:
```
AUTH_TOKEN = '<your_token>'
NAMESPACE = '<your_namespace>'
```

Выполнить:
```
$./virtualenv-setup.sh --dev
```

Тестировать:
```
$env/bin/py.test tests/
```
