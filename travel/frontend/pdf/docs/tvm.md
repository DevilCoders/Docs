## Конфигурирование tvm через bash

Конфиг TVM `/etc/tvmtool/tvmtool.conf`: шаблон `tools/tvm/tvm.blank.json`.

Значение поля `secret` берем из [секретницы](https://yav.yandex-team.ru/?role=reader&search=2010566).

Редактируем файл `/var/lib/tvmtool/local.auth`

```
$ sudo vim /var/lib/tvmtool/local.auth
```

Заменяем содержимое на:

```
41111111111111111111111111111111
```

Перезагружаем TVM

```
$ sudo service yandex-passport-tvmtool restart
```
