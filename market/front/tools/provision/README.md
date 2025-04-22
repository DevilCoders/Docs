provision
---------

Cодержит роли для `ansible provisioning`-серверов.

На данный момент из него наливаются:
- `logrus*` железные разработческие машины.

### Как раскатить изменения

**Написать в [чат дежурному](https://t.me/joinchat/C5yyIUy9ythghPB6TfsD7w). Ни в коем случае не выкатывайте самостоятельно. Некоторые сценарии требуют особых прав, без которых есть шанс поломать работу логрусов**

#### Инструкция для дежурного

**Важно: в скриптах используется python2.7**

Первая настройка:
```sh
./setup-and-install.sh
```

Если упало с ошибкой `ERROR! Unexpected Exception: invalid syntax (posix.py, line 66)`, то ты запустил установку с `python3`.

Можно попробовать явно указать версию пайтона:
```
virtualenv venv --python=/usr/bin/python2.7
```

Если ошибка такого рода: `fatal error: Python.h: No such file or directory`
то можно попробовать:
```sh
sudo apt-get install python-dev   # for python2.x installs
sudo apt-get install python3-dev  # for python3.x installs
```
и перезапустить терминал

Если у вас все настроено и надо только раскатить:
```sh
source venv/bin/activate
./install.sh
```

Если запрашивает согласие на подключение к логрусу, то отключить StrictHostKeyChecking в config от ssh. Должно получиться что-то такое:
```
Host logrus*
  ForwardAgent yes
  StrictHostKeyChecking no
Host market.logrus*
  ForwardAgent yes
```

**секрет**

Если файлики секретов не обновились (но вообще должны), то на логрусе нужно вызвать `sudo yav-deploy`.

### См. также
- [Контрибьютинг в репозиторий](CONTRIBUTING.md)
