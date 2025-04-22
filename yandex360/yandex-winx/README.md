yandex-winx
===========

# Админка саппортов почты.

* Сборка в Jenkins: https://common.jenkins.mail.yandex.net/job/mail-support/job/yandex-winx/
* Окружение в Qloud: https://platform.yandex-team.ru/projects/mail/magic

## Быстрый старт

Для разработки требуется разработческая виртуалка в сети \_MAILTESTNETS_.
Как её завести описано [тут](https://wiki.yandex-team.ru/pochta/backend/newman/virtual/).

1. Настраиваем arc на qyp машинке. Идем в `~/arcadia/yandex360/yandex-winx`
2. Настраиваем docker compose по доке docs/docker.md
3. Подставляем дев конфиг для docker compose: `cp docker-compose.dev.yml docker-compose.override.yml`
4. Запускаем миграции, обязательно создаем пользователя `root`
```
cd ~/magic
docker compose run magic /app/manage.py syncdb --noinput
docker compose run magic /app/manage.py migrate yandex_winx_admin
```
5. Добавляем настройки TVM в `src/yandex_winx/secure_settings.py`:
```
TVM_CLIENT_ID = 2002384
TVM_SECRET = '<testing secret>'
```
6. Запускаем приложение
`docker compose up`
7. Пробрасываем порт на рабочий ноут `ssh -L 8080:127.0.0.1:80 <fqdn_dev>`
8. Открываем в бразуре http://localhost:8080/

## Локальный поход в BB
1. В `env/lib/python2.7/site-packages/blackbox.py:293` добавить:
```python
            conn = cls('127.0.0.1', 4444, timeout=timeout)
            conn.set_tunnel(parts.hostname, 80)
            import socks
            conn.sock = socks.socksocket()
            conn.sock.set_proxy(socks.PROXY_TYPE_SOCKS5, "127.0.0.1", 4444)
            conn.sock.connect((parts.hostname, 80))
```
2. Запустить `make tunnel`
