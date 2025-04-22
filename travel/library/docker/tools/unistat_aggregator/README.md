==Что это
Простой сервис, который имитирует push-api голована с одной стороны и unistat ручки с другой.
https://doc.yandex-team.ru/Search/golovan-quickstart/concepts/push.html - описание push api
https://wiki.yandex-team.ru/golovan/stat-handle/?from=%252Fjandekspoisk%252Fsepe%252Fmonitoring%252Fstat-handle%252F -
    описание unistat формата

==Как обновить
Поднимаем version в setup.py и выполняем
`python setup.py sdist upload -r yandex`

username и password нужно получить тут https://pypi.yandex-team.ru/accounts/access-keys/

При условии, что в ~/.pypirc есть секция
```
[distutils]
index-servers =
    yandex

[yandex]
repository: https://pypi.yandex-team.ru/simple/
username: {some-long-string}
password: {some-another-long-string}
```

==Использование
Установка:
`pip install unistat_aggregator`

Запуск:
`unistat_aggregator`

Возможные параметры:
  --port (переменная окружения UNISTAT_PORT) - на каком порту слушает
  --override-tags (переменная окружения UNISTAT_OVERRIDE_TAGS) - следует ли добавлять тэги к именам сигнала
