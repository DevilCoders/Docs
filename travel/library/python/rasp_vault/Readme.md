## Секретница

https://vault-api.passport.yandex.net/docs/  
https://yav.yandex-team.ru

## Как обновить
Поднимаем version в ``rasp_vault.__init__`` и выполняем
``python setup.py sdist upload -r yandex``

Затем ``./releasedeb.sh`` для сборки deb пакета

username и password нужно получить тут https://pypi.yandex-team.ru/accounts/access-keys/

В ~/.pypirc должна быть секция
```
[distutils]
index-servers =
    yandex

[yandex]
repository: https://pypi.yandex-team.ru/simple/
username: {some-long-string}
password: {some-another-long-string}
```

## Экспорт настроек

Можно посмотреть какие настройки выгрузятся командой ``print``

```
$ rasp-vault print -t production
<rasp-common-mongo: sec-01cma58wwavd78bm1phjtpwzp6 ver-01cma5kbeb69cr5nt5pcb3t18x; (u'mongodb', u'production', u'testing')>
<rasp-common-mysql: sec-01cma50anqzshpfj1fg45zmzhd ver-01cma50anvztsnq627b1mnkyaa; (u'mysql', u'production', u'testing')>
```

Теги можно компоновать операторами из python, ``` (), and, or, not```,
 в связи с этим теги должны быть вылидными именами, ``-`` заменяются на ``_``,
 поэтому минус тоже можно использовать в тегах.

```
$ rasp-vault print -t '(production and mysql) or not robot'
<rasp-common-mongo: sec-01cma58wwavd78bm1phjtpwzp6 ver-01cma5kbeb69cr5nt5pcb3t18x; (u'mongodb', u'production', u'testing')>
<rasp-common-mysql: sec-01cma50anqzshpfj1fg45zmzhd ver-01cma50anvztsnq627b1mnkyaa; (u'mysql', u'production', u'testing')>
<ya-upload-mds: sec-01ckx62bkvpee201ks4d4a1g09 ver-01ckx62bm2j00f44sag2910hn4; (u'ya',)>
<rasp-sentry: sec-01chhx6gejynq4aaxd5p80b10c ver-01cj4ejkfej9bmzhvjappjatvc; ()>
```

Можно добавить секреты по их алиасу.

```
$ rasp-vault print -t '(production and mysql)' --extra rasp-sentry
<rasp-common-mysql: sec-01cma50anqzshpfj1fg45zmzhd ver-01cma50anvztsnq627b1mnkyaa; (u'mysql', u'production', u'testing')>
<rasp-sentry: sec-01chhx6gejynq4aaxd5p80b10c ver-01cj4ejkfej9bmzhvjappjatvc; ()>
```

Для экспорта в qloud нужно использовать команду ``qloud-export``,
аргументы такие же как и в команде ``print``.
Так же можно указать ширину строки base64
 
```
$ rasp-vault qloud-export -t '(production and mysql)' --extra rasp-sentry --line-limit 180
H4sIAG4mcVsC/31STY/aMBC9769AVEiVWqSYzWdPLFBAC6LQAgl7qOUkJonjJI6dT1b89ya72iWHios1njczb96zXx96vT5Hgg2dJIqSeBjVIqX9H73XBmgggR2Os+beRkMJOBFSJBSnF+GzMwFnT1Yu0cV3+9977w0F5iJI4rajCW8dxSUT
caqONBtEcVgjdOtANMefjE2CISHKhLvtjArhNNcZmn2UN3guMG+xdu3+W/LanNe3gnctAscZr++o8P1K9TCp41RGqHIVpks2kJw7KoiMSXjGxLAbuQVBjBGUFc4dFR5CAjKeuLmTNbNgZzMIXRt+yIQty+V0yn1vZeiLk6NOCfXMrbHTQ3NP
ZWwas8Wj8bQFMlkvtme0pcC3fi8lbim5Hmh/OtbchAaDUDf438GYurQafSvDgaIpYxeNfDwMS4R4jvmXr8Y5HY+DSqViILpjcoY5bH2GkCd2kg3b5SHsvgwfGWwDnqoEEE1amYdfjz+NNbCfD7YqzY75tNBqidQzOl1VgSzUZycvlkun2IMJ
m3SoGpuEgDDDIgtiD/7XpU/OInspD+ulL0YoWFqb0ATWXjLDffyyU/S9VezmxPeK48ICRrQ4TDY6y+bSsdSoPqedn/Jw/QfvC2Xb9wIAAA==
```

Для экспорта в admin нужно использовать команду ``file-export``,
аргументы такие же как и в команде ``print``.
Так же можно указать файл для экспорта, по умолчанию ``/etc/yav-secrets/rasp.json.gz``
 
```
$ rasp-vault file-export -t '(production and mysql)' --extra rasp-sentry --file 1.json.gz
```

## Использование ``api``

Использовать можно как по алиасам так и по id секретов.
Можно указывать полный путь к секрету, либо только ключ(secret_uuid).

```python
from rasp_vault.api import get_secret

get_secret('alias.key')  # 'some_key'
get_secret('sec01afsdf.key')  # 'some_key'

get_secret('sec01afsdf')  # {'key', 'some_key' ...}
get_secret('alias')  # {'key', 'some_key' ...}
```

## Использование ``api`` без файлов ``/etc/yav-secrets/``

**Каталога ``/etc/yav-secrets/`` не должно быть на машинке, иначе будут использоваться файлы из каталога!**

Если запускаете программу от себя, то api может использовать ключ агента, чтобы получить секрет.
Для этого нужно настроить ssh агента у себя на машинке.

Это можно сделать добавив в ``.bashrc``
```bash
agent_sock_file=~/.ssh-agent.socket
agent_pid_file=~/.ssh-agent.pid

touch $agent_sock_file
touch $agent_pid_file

if [ \( -n "$(cat $agent_sock_file)" \) -a \( -n "$(cat $agent_pid_file)" \) -a \
    \( -e "$(cat $agent_sock_file)" \) ] && ps ax | grep "$(cat $agent_pid_file) .*ssh-agent" > /dev/null
then
    echo Agent already started
    export SSH_AUTH_SOCK=$(cat $agent_sock_file)
    export SSH_AGENT_PID=$(cat $agent_pid_file)
else
    echo Starting ssh agent
    eval $(ssh-agent)
    echo $SSH_AUTH_SOCK > $agent_sock_file;
    echo $SSH_AGENT_PID > $agent_pid_file
fi

ssh-add ~/.ssh/yandex_rsa &> /dev/null
ssh-add ~/.ssh/bitbucket_rsa &> /dev/null
```

B конфиг ``~/.ssh/config``, либо логиниться через ssh -A 
```
ForwardAgent yes
```

Если заполнена переменная окружения RASP_VAULT_OAUTH_TOKEN, то ключ агента будет игнорироваться и
будет использоваться токен. Для запуска через pycharm можно добавить его в environment переменную конфигурации.
[Получить токен секретницы.](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982)

Так же можно сделать файлик в домашней директории ``~/.rasp_vault_token`` **с правами ``400``**.
 Чтобы не менять все настройки в PyСharm.


## Как заводить секреты

Секреты мы называем ``rasp-<project>-<evironment>-<type>``
например,  
* ``rasp-common-misc`` - для всех проектов и для всех окружений,  
* ``rasp-train_api-production-trust`` - для train_api production.

На секрет, нужно дать права на наши группы в стафе и роботу.
Это можно сделать в консоли. Проверяйте, что доступ выдан на нужные группы.

```bash
s='<secret-key>'; yav update secret $s -r +owner:staff:37453 +owner:staff:37454 +reader:user:robot-rasp

# Этой командой можно проверить, на какие секреты у вас есть доступ,
# а у робота нет прямого доступа.
rasp-vault print --no-access-from-user=robot-rasp
````


## Перемещение пакета в testing, stable

Чтобы пакет можно было ставить в тестинге или проде, его нужно переместить в нужный репозиторий

```bash
ssh yandex-rasp-trusty.dupload.dist.yandex.ru

sudo dmove yandex-rasp-trusty testing yandex-rasp-vault '<version>'
```


## Выпуск обновление выгрузки секретов в qloud

**Важно!!!** Не удаляйте и не изменяйте старые ключи, сначала нужно сделать новый ключ в секрете, перейти на него,
 потом уже можно редактировать не используемые ключи.

Секреты должны в qloud именоваться примерно так ``vault-rasp-common-production-2018-08-17``,
 где дата когда вы создали секрет. rasp-common - это репозиторий.

Файл куда попадет секрет можно именовать похожим образом ``/etc/yav-secrets/rasp-common-production.json.gz``.

Тип секрета нужно выбирать binary/base64.

Так же при выпуске нового секрета в qloud, нужно убедиться что секрет доехал до всех окружений,
это можно сделать командой.

```bash
rasp-vault need-secret --token='<token>' rasp vault-rasp-common-production-2018-08-17 | grep -E 'testing|prestable|production'
```

Токен так же можно передать через переменную окружения ``QLOUD_API_TOKEN``.


## Запуск джанговских скриптов в Dockerfile

Секреты чаще всего не доступны и не нужны в Dockerfile или в тестовых окружениях,
и чтобы get_secret не ходит за секретами,
нужно установить переменную окружения ``RASP_VAULT_STUB_SECRETS=1``
