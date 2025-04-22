# Пример конфигурации для ванильного OpenSSH сервера

Самое вкусное находится в:
  - основной конфиг, который говорит sshd как дружить с SSH PKI `etc/ssh/sshd_config.d/01_skotty.conf`
  - и пример запуска, с добавлением разных пользователей: `start.sh`

В остальном все доволльно штатно.

# Пример запуска

```
# собираем образ
$ docker build -t sshd_example .

# запускаем с добавлем себя в качестве без рутового пользователя
$ docker run -it -e CAT_LOGIN="$USER" -p 127.0.0.1:2222:22/tcp sshd_example:latest
# логинимся
$ ssh localhost -p 2222

# или запускаем с добавлением себя в качестве пользователя с возможностью логиниться рутом
$ docker run -it -e SUPER_CAT_LOGIN="$USER" -p 127.0.0.1:2222:22/tcp sshd_example:latest
# теперь можем логиниться как под собой
$ ssh localhost -p 2222
# так и под рутом
$ ssh localhost -p 2222 -l root
```

# Что осталось за скобками
  - периодический синк `/etc/ssh/pki/users_ca` и `/etc/ssh/pki/users_krl`
  - парольное sudo
