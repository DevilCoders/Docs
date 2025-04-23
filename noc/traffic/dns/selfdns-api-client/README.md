# selfdns-api-client

Клиент [[1]](https://wiki.yandex-team.ru/dynamic-dns/selfdns-api/) для сервиса selfdns, позволяющий прописать хост в зонах dns (обратных и прямых) и поддерживать такое соответствие.

### зависимости:
>[~] arcadia, ya

### если ломаем совместимость:
Если делаем изменения, которые несовместимы с текущей версией, обязательно инкрементируем версию:
- в файле `internal/config/version.go` переменная `apiVersion`
- в файле `debian/changelog`

### использование Sandbox для сборки
1. открываем https://sandbox.yandex-team.ru/task/1216270852/view
2. наверху справо среди кнопок выбираем Clone
3. пишем в Description с чем связана новая сборка и не меняя остальных настроек нажимаем Run
4. по окончанию работы таски(SUCCESS наверху рядом с названием таски) пакет будет в common unstable

### тестирование
- используется робот https://staff.yandex-team.ru/robot-dnsapi-test 
- тестировать можно на `build-bionic-01i.cdn.yandex.net`
- токен для тестирования тут https://yav.yandex-team.ru/secret/sec-01fttbe22zr1dn97fq8rw37ppr/explore/versions

### сборка на ноутбуке для linux
>[~] ya make

### сборка на ноутбуке для windows
>[~] ya make --target-platform=windows

### собрать и подписать deb пакет:
>[~] ya package --debian package.json --not-sign-debian -Z=gzip
>[~] debsign -k LOGIN@yandex-team.ru *.changes

### собрать tar пакет c бинорями для windows:
>[~] ya package --tar package_windows.json

### возможности запуска клиента описаны в его help:
>[~] selfdns-client --help

>     This program is a client for selfdns-api.

>     selfdns-client [--config][--debug][--terminal]

>       [--logfile][--plugins-dir]
>       [--plugins-enabled]
>       [--token|--notoken]
>       [--timeout]
>       [--version]
>
>     DEFAULT VALUES
>       config = /etc/yandex/selfdns-client/default.conf
>       logfile = /var/log/yandex-selfdns-client/client.log
>       All other you may see in config file.
>
>     SEE INFO HERE
>       [1] https://wiki.yandex-team.ru/dynamic-dns/selfdns-api
>
>     USAGE EXAMPLES
>       a) debug mode without token for checking connection with server and config file, log to terminal:
>           selfdns-client --debug --terminal --notoken
>       b) redefined config:
>           selfdns-client --config $HOME/selfdns-client.conf
>       c) change token and plugins:
>           selfdns-client --token 01114567890111456789 --plugins-enabled default,users_plugin
>       d) command-line only run:
>           selfdns-client --debug --terminal --token 01114567890111456789 \
>               --plugins-enabled default --plugins-dir /etc/yandex/selfdns-client/plugins \
>               --timeout=10
>
>     SELFDNS-CLIENT VERSION: "0.2.8"


* debian пакет включает в себя крон-задачу, которая раз в 5 минут запускает selfdns-client, он посылает текущее состояние списка имён хоста и его ip адресов, сервис, в свою очередь, вычисляет нужно ли что-то изменить в соответствующих зонах и применяет изменения.

* при установке пакет создаёт системного пользователя selfdns из под которого работает крон-задача

----
**[1]**  [https://wiki.yandex-team.ru/dynamic-dns/selfdns-api](https://wiki.yandex-team.ru/dynamic-dns/selfdns-api/)
