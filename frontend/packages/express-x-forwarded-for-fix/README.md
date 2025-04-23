# express-x-forwarded-for-fix [![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/express-x-forwarded-for-fix/status.svg)](https://drone.yandex-team.ru/toolbox/express-x-forwarded-for-fix) [![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/packages/express-x-forwarded-for-fix&vcs=arc)](https://oko.yandex-team.ru/repo/toolbox/express-x-forwarded-for-fix)

Исправляем заголовок X-Forwarded-For.

Middleware фильтрует из заголовка вхождения (разделенные запятой) не похожие на
IP адрес, а так же [зарезервированные адреса](http://ru.wikipedia.org/wiki/IPv4#.D0.97.D0.B0.D1.80.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B0.D0.B4.D1.80.D0.B5.D1.81.D0.B0) (пока только из IPv4).

Так же поддерживает значение заголовка `X-FORWARDED-FOR-Y` (специальный, Яндексовый).

Установка
---------

```npm install express-x-forwarded-for-fix --registry=http://npm.yandex-team.ru/```

Параметры
---------

* `filterReserverd` - убирать зарезервированные IP адреса (default: `true`)
* `defaultIP` - Адрес по умолчанию, если все остальные были отфильтрованы (default: `process.env.XFF_DEFAULT_IP`), полезно для отладки.
* `allowedNetMasks` — Позволяет разрешить подсети по маске (позволяет разрешить и адреса из зарезервированных).

Пример
------

```javascript
var app = express();

// Для определения ip адреса пользователя по X-Forwarded-For
app.enable('trust proxy');

// Убираем мусор из X-Forwarded-For (например undefined) и зарезервированные адреса
app.use(require('express-x-forwarded-for-fix')());
// или только мусор
app.use(require('express-x-forwarded-for-fix')({
    filterReserved: false
}));
// или разрешаем одну из зарезервированных подсетей
app.use(require('express-x-forwarded-for-fix')({
    allowedNetMasks: ['198.18.0.0/15']
}));
```
