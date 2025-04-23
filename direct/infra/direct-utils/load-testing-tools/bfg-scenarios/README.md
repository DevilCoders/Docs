# Сценарии для нагрузочного тестирования

## Перед запуском

Перед тем, как заводить танк, его нужно правильно сконфигурировать. Для этого достаточно дописать несколько строк в `load.ini`

```
[meta]
operator=<ваш логин в yandex-team, например, elwood>

[ultimate_gun]
token=<токен какого-нибудь супера на бетах>
client_login=<логин произвольного клиента, который есть в БД стенда, например, boschbuy>
java_api_url=http://ppctest-ts3-front.ppc.yandex.ru:10181
old_api_url=https://ppctest-ts3-front.ppc.yandex.ru:14443
use_always_old_api=False
```

И указать в файле `ammo.txt`, какие сценарии нужно вызывать:

```
case1\tmissile1
case2\tmissile2
```

Где

`case1` - имя метода сценария,

`missile1` - строка, которая будет передана методу в качестве аргумента

`\t` - символ табуляции (именно табуляции - это важно!)


## Как запустить через Docker

```bash
docker build -t 'tank:my' .
docker run -v $(pwd):/var/loadtest --privileged --net host -it tank:my bash -c 'cd /var/loadtest && PYTHONPATH=$(pwd):$PYTHONPATH yandex-tank -c load.ini'
```

## Как запустить локально

1. Установить Python 2.7 (например, в virtualenv)
2. Обновить setuptools

```bash
pip install --upgrade setuptools
```

2. Установить Yandex Tank

```bash
pip install https://api.github.com/repos/yandex/yandex-tank/tarball/master
```

3. Запустить стрельбу

```bash
PYTHONPATH=$(pwd):$PYTHONPATH yandex-tank -c load.ini
```
