# express-ya-frameguard
Yandex Aware frameguard.

Предотвращает показ страницы в iframe путем установки заголовка X-Frame-Options, если ее смотрят не из яндексовой сети.
Такой костыль нужен для того, чтобы сотрудники яндекса могли просматривать страницу в вебвизоре.

## Использование
Для работы нужен express-http-geobase (либо другим способом создать объект req.geolocation и выставить в нем поле is_yandex
при заходе с яндексовой подсети).

```
app.use(require('express-http-geobase')());
app.use(require('express-ya-frameguard')());
```

В экспортируемую функцию инициализации можно передать объект с опциями:
- `header` - значение заголовка X-Frame-Options - deny/sameorigin/allow-from,
- `allow_from` - если 'header' == 'allow-from', то в эту опцию нужно передать, на какой странице разрешено встраивание.
