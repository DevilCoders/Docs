Описание
====
Утилита для парсинга тикетов с заявками и складывания их [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/recomposing)

Запуск
====

```
- ya make
- ./recompose --token <token> --main-ticket <startrek-ticket-slug>
```
Если в тикетах нет пункта "Когда будут нужны ресурсы" дополнительно нужно передать параметр --month (int)

Например, для RVL-2:
```
- ya make
- ./recompose --token <token> --main-ticket RVL-2 --month 5
```
токен должен давать права на YT и startrek
