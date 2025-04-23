# Библиотека полезных запросов

> Цель: саккумулировать знания о метриках и логах в одном месте для наращивания экспертизы.

## Как это работает?

Полный список для удобного поиска доступен на Вики странице (https://wiki.yandex-team.ru/market/frontend/infra/yql/).

## Контрибьют

Содержимое Вики-страницы генерируется из этого репозитория. Поэтому нельзя редактировать контент именно в Вики.

После редактирования содержимого библиотеки, нужно воспользоваться командой `yammy build @yandex-market/queries`.

## Структура и требования

Запросы описываются через Markdown.

Шапка (вступление) лежит в отдельном файле ([src/content/readme.md](./src/content/readme.md)).

Каждый запрос должен иметь:
- название
- описание
- набор тегов
- ссылку с этим запросом в интерфейсе YQL

Все это нужно для быстрого поиска и удобства запуска.

## Полезные практики синтаксиса Clickhouse

Желательно, чтобы код запроса должен быть агностик, мог быть выполнен всегда.

### Интервал во времени

По часам:
```sql
timestamp between toDateTime(now() - interval '2' HOUR) and toDateTime(now())
```

По дням:
```sql
date between toDate(now() - interval '2' DAY) and toDate(now())
```

## Благодарность

Большое спасибо за развитие культуры запросов. Первые запросы собраны, благодаря коллегам:
- Михаил Силаев [@gheljenor](https://staff.yandex-team.ru/gheljenor)
- Павел Верба [@lisenque](https://staff.yandex-team.ru/lisenque)
- Павел Ляхов [@lengl](https://staff.yandex-team.ru/lengl)
- Дмитрий Поляков [@polyakovda](https://staff.yandex-team.ru/polyakovda)
- Данила Авдошин [@avdotion](https://staff.yandex-team.ru/avdotion)
