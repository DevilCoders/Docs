# RUM

## [rum-counter](https://github.yandex-team.ru/RUM/rum-counter)

Реализует сбор и отправку метрик скорости загрузки интерфейса.

[Дашборд](https://rum.yandex-team.ru/projects/realty/projectDashboard)

### Вручную добавленные метрики

_first meaningful paint_. Время отображения основного элемента страницы. Задается в виде соответсвия "страница" -> "селектор основного элемента" в файле `realty-core/app/lib/rum-counter/utils.js`

### Debug

Для отладки событий rum-счетчика есть специальный get-параметр "__rum_debug=1". Доступно в деве и тестинге. 

## [error-counter](https://github.yandex-team.ru/RUM/error-counter)

Реализует отправку клиентских ошибок поверх RUM счетчика.

[Дашборд](https://error.yandex-team.ru/projects/realty/projectDashboard)

## Дашборд

### Выборка по дополнительным параметрам

Вместе с данными метрик можно передавать произвольные параметры. Чтобы в дашборде отфильтровать по ним нужно сделать запрос вида:
```
additionalKeyValue in "userType: AGENCY"
```

В данный момент передаются следующие доп. параметры: userType, uid.
