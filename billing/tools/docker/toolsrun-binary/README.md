# образ контейнера для запуска сервантов баланса
Образ содержит полный фарш (xscript, corba, nginx, nodejs) для запуска сервантов.

# как пользоваться
Контейнер работает с локальной копией баланса.
```bash
#запускаем bootstrap и прочее
docker run --rm --name toolsrun -v ~/tools:/tools registry.yandex.net/balance/toolsrun:trusty /build.sh
#запускаем серванты
docker run -d -P --name toolsrun -v ~/tools:/tools registry.yandex.net/balance/toolsrun:trusty
```
на запуск потребуется некоторое время, сервантов много. Контейнер будет слушать следющие порты:
```
medium      8003 http
test-xmlrpc 8005 http
balance-user 8088 https
balance-admin 8089 https
```
Порты с ssl используют самоподписанные сертификаты. Чтобы подсунуть в контейнер валидные сертификаты, нужен параметр `-v ssl:/etc/nginx/ssl`. Файлы в директории ssl:
```
server.crt
server.key
```

Чтобы на хостах с ipv6-only для проброса сети в контейнер проще всего использовать MASQUERADE. Но тогда перестаёт работать логин из y-t.ru, т.к. до приложения не доезжает клиентский IP, а он сильно нужен доменному паспорту.
Для обхода, в nginx прибивается адрес одного из серверов. Его лучше переопределять адресом текущего хоста.
```
docker run -e "NGINX_REMOTE_ADDR=`hostname -i | head -n1`" ...
```

Custom tns is not supported right now <del>Если нужно переопределить базу в которую ходит контейнер, то нужно запустить что-то типа</del>
```bash
docker run --rm --name toolsrun -v ~/tools:/tools -e DOCKER_BALANCE_DB=DEV_BALANCE_YANDEX_RU registry.yandex.net/balance/toolsrun:trusty /build.sh
```
По дефолту контейнер идёт в разработческую базу

Если нужно пойти в докер-контейнер с базой оракла, то в tnsnames-virtual.ora есть специальная запись VIRTUAL, которую можно использовать, если при запуске контейнера указать --link orcl:orcl

Стоит учесть, что авторизация в вёрстке не будет работать, если домен не yandex(-team)?.ru. Чтобы обойти это ограничение, можно передать в контейнер переменную окружения: ```FORCE_SKIP_CHECKAUTH_UID=<UID>```. Тогда авторизация в верстке не потребуется.
