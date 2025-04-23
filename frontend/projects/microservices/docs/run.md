# Инструкция по запуску микросервисов

## Установка
1. Склонировать репозиторий с микросервисами https://github.yandex-team.ru/search-interfaces/microservices
2. Перейти в директорию с микросервисами `cd microservices`
3. Установить зависимости `npm i`

## Запуск 
### Способ 1. Локальный запуск
1. Запустить необходимый микросервис `npm run (prosperity|merge-queue|webhook-handler|sandbox-ci)`
2. Для запуска будет запрошен пароль https://yav.yandex-team.ru/secret/sec-01d80wnwn8mr5evsws5tcvt8gk

### Способ 2. Запуск в Docker-контейнере
1. Запустить Docker
2. В директории с микросервисами запустить сборку контейнера `make docker-build`
3. После сборки запустить контейнер с указанием сервиса, например, так `make SERVICE=merge-queue docker-run`
4. Во время запуска будет запрошен пароль для расшифровки конфигурационного файла, пароль можно взять отсюда https://yav.yandex-team.ru/secret/sec-01d80wnwn8mr5evsws5tcvt8gk

## Настройка хуков на GitHub

Для проверки интеграции с GitHub, нужно в репозитории (например, своём форке web4) настроить хуки на свою локальную версию микросервисов.

Чтобы GitHub смог достучаться до локального сервиса, необходимо настроить ssh-тоннель, который будет проксировать трафик от GitHub через сеть, до которой у GitHub есть доступ.

Посмотреть правила фаервола, которые настроены для GitHub, можно в [Golem](https://golem.yandex-team.ru/fwparser2.sbml?query_mode=hardcore&group_mode=AND&sort_by_relevance=0&from=*&to=*&q=github.yandex-team.ru).

> Например, `_SEARCHSAND_` — сеть, в которой живут виртуальные машинки разработчиков Поиска. До неё есть доступ.

Соответственно, сперва нужно [создать виртуальную машину](https://wiki.yandex-team.ru/search-interfaces/infra/infraspeed/docs/sandbox-ci/local-sandbox/#podnimaemmashinkuvopenstack) в этой сети, через которую будет проксироваться трафик.

Заходим на эту машину по `ssh` (публичный ключ должен быть указан на staff-е).

По умолчанию `ssh` не разрешает проксировать трафик, чтобы это [поправить](https://gist.github.com/theycallmeS/7040944), нужно добавить `GatewayPorts yes` в файлик `/etc/ssh/sshd_config` и перезапустить ssh-сессию `sudo service ssh restart`.

> **Важно**
>
> Текущие правила фаервола разрешают соединения только на 6000-9000 портах.

Запускаем тоннель на 9000 порту:

```
$ ssh -R 9000:localhost:3000 -N {user}@{host} -v   
```

где `localhost:3000` — адрес локально запущенного микросервиса.

В консоли должны увидеть лог:

```
debug1: Remote connections from LOCALHOST:9000 forwarded to local address localhost:3000
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: Remote: Forwarding listen address "localhost" overridden by server GatewayPorts
debug1: remote forward success for: listen 9000, connect localhost:3000
debug1: All remote forwarding requests processed
```

Запускаем микросервис и проверяем, что всё работает:

```
$ curl -v http://{host}:9000

* Trying ...
* Connected to {host}
```

Дальее настраиваем хуки на GitHub, используя вышеуказанный `host`.
