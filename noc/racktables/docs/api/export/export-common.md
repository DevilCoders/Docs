# Export

## Основное
`/export` доступен для использования вне-НОК. Дергает напрямую выделенные ручки `php`

[Список экспортов в репозитории Gitlab](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/tree/master/export)

## Использование
Для использования достаточно пойти на `URL Racktables` + `/export/` + `название_нужной_ручки.php` + `?` + `параметры_запроса`

URL Racktables:
* Чтение - `ro.racktables.yandex-team.ru`
* Запись - `racktables.yandex-team.ru`

{% cut "Пример" %}

Выгрузить все ipv4 сети
```
white-osx2:~ white$ curl https://racktables.yandex-team.ru/export/allipv4nets.php?format=allipv4nets
0.0.1.0/24
5.45.192.0/18
5.45.192.0/24
~cut
217.169.82.4/31
217.169.82.160/27
217.173.74.64/29
```

{% endcut %}