# Прокси для доступа к ipv6 адресам

## Что это и для чего нужно
Демон docker-а не может обращаться к ipv6 из контейнера на mac os.
Подробности https://github.com/docker/for-mac/issues/1432

Данная прокся редиректит c ipv4 адрес на ipv6.

## Как это работает?
Proxy осуществляет редирект по пути указанной в подстроке `redirect-path` `podrick.c.maps.yandex-team.ru/proxy/<redirect-path>`

Заголовки запроса, порт,
`podrick.c.maps.yandex-team.ru/proxy/blackbox.yandex-team.ru:443 -> blackbox.yandex-team.ru:443`

и query-параметры передаются в неизменном виде.
`podrick.c.maps.yandex-team.ru/proxy/blackbox.yandex-team.ru/?param=1 -> blackbox.yandex-team.ru?param=1`

Для использования в приложении, просто нужно в конфиге приложения изменить ipv6 хост
на адрес прокси подрика.
`blackbox.yandex-team.ru -> podrick.c.maps.yandex-team.ru/proxy/blackbox.yandex-team.ru`

## HTTP(S)

Если вам надо использовать только HTTP или HTTPS хост, то протокол надо передавать вначале запроса.

Сравните:

`http://podrick.c.maps.yandex-team.ru/proxy/somehost.ru/ -> http://somehost.ru/`

`https://podrick.c.maps.yandex-team.ru/proxy/somehost.ru/ -> https://somehost.ru/`

## Внутренний Blackbox

При обращених к внутреннему ЧЯ необходимо указывать `userip` из внутренней сети. Но при локальной разработке `usepip` – 127.0.0.1, поэтому ходить напрямую в ЧЯ не получается.

Для походов во внутренний ЧЯ при локальной разработке используйте `podrick.c.maps.yandex-team.ru/blackbox-int/`. Этот прокси заменяет `userip` на реальный ваш IP. Все остальные параметры проксируются без изменений.

```
http://podrick.c.maps.yandex-team.ru/blackbox-int/blackbox?sessionid=3:14029...&host=yandex.ru&userip=127.0.0.1 ->
http://blackbox.yandex-team.net/blackbox?sessionid=3:14029...&host=yandex.ru&userip=12.12.12.12
```