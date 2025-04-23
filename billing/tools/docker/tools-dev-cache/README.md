# Образ контейнера для кеширования toolsrun при разработке frontend

На данный момент реализовано только для админки. Кеширование реализовано с использование сервиса [varnish](http://book.varnish-software.com/4.0/).
Вся настройка в `default.vcl`.

Cookie `balance.dev` для разработки проставляются автоматически.

## Как пользоваться

* Развернуть контейнер toolsrun

* Уточнить IP адрес, на котором развернута админка toolsrun:

```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' toolsrun
```

* Полученный IP подставить в параметр `host` в `default.vcl`.

* Собрать образ и запустить контейнер:

```
docker build -t tools-varnish .
docker run -itd -p 8082:6081 --name running-tools-varnish tools-varnish
```

* Открыть `http://localhost:8082`

## Как сбросить кеш

Отправить запрос с методом PURGE на `http://localhost:8082` либо с любым методом на URL `http://localhost:8082/clear-cache`