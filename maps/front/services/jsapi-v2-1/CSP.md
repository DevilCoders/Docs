# CSP Политика

Документ описывает csp политику и изменения, происходящие в ней со временем.
Суть проблемы:

1. Мы опубликовали документацию по csp с определенным набором правил (v1).
2. Пользователи взяли этот набор и подключили jsapi с csp и у них все работает.

<b>ВАЖНЫЙ ВЫВОД: С этого момента мы неявно обязались гарантировать, что вся функциональность, которая была в jsapi на момент публикации csp правил, продолжит работать с этими правилами в будущих версиях jsapi.</b>

Поэтому мы можем расширять требования для csp строго для новой функциональности, которой не было в версиях до 2.1.62.
В общей документации на tech мы сразу пишем расширенные требования, чтобы новые пользователи не задумывались о том, какие конкретно правила им пригодятся в будущем.
К этому надо очень внимательно относиться и не забывать, что расширенные требования по csp не прописаны у старых пользователей (у них на сайте скопирована версия v1).

Можно в query параметрах подключения jsapi указать версию CSP политики.
Это не публичный параметр. Используется только для Яндексовых сервисов.
```
https://api-maps.yandex.ru/2.1/?csp[version]=${version}
```

## v3 (версия 2.1.77, изменения от 22 июня 2020)

#### Изменения

Добавили `yastatic.net` в `script-src`.

#### Правила
    Content-Security-Policy:
        img-src data: https://*.maps.yandex.net https://api-maps.yandex.ru https://yandex.ru 'self';
        child-src https://api-maps.yandex.ru;
        frame-src https://api-maps.yandex.ru;
        script-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru http://*.maps.yandex.net https://yandex.ru https://yastatic.net 'self';
        connect-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru https://*.maps.yandex.net https://yandex.ru https://*.taxi.yandex.net;
        style-src blob:;


## v2.2 (версия 2.1.73, изменения от 14 февраля 2018)

#### Изменения

Добавили апи такси в connect-src.

#### Правила
    Content-Security-Policy:
        img-src data: https://*.maps.yandex.net https://api-maps.yandex.ru https://yandex.ru 'self';
        child-src https://api-maps.yandex.ru;
        frame-src https://api-maps.yandex.ru;
        script-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru http://*.maps.yandex.net https://yandex.ru 'self';
        connect-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru https://*.maps.yandex.net https://yandex.ru https://*.taxi.yandex.net;
        style-src blob:;

## v2.1 (версия 2.1.64, изменения от 17 апреля 2018)

#### Изменения

Ослабили политику, убрали `script-src 'unsafe-eval'`.

#### Правила
    Content-Security-Policy:
        img-src data: https://*.maps.yandex.net https://api-maps.yandex.ru https://yandex.ru 'self';
        child-src https://api-maps.yandex.ru;
        frame-src https://api-maps.yandex.ru;
        script-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru http://*.maps.yandex.net https://yandex.ru 'self';
        connect-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru https://*.maps.yandex.net https://yandex.ru;
        style-src blob:;

## v2 (версия 2.1.62, изменения от 15 марта 2018)

#### Изменения
Добавили `connect-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru https://*.maps.yandex.net https://yandex.ru` для модуля регионов (версия 2) и для реализации дальнейших планов по отказу от jsonp.

#### Правила
    Content-Security-Policy:
        img-src data: https://*.maps.yandex.net https://yandex.ru 'self';
        child-src https://api-maps.yandex.ru;
        frame-src https://api-maps.yandex.ru;
        script-src 'unsafe-eval' https://api-maps.yandex.ru https://suggest-maps.yandex.ru http://*.maps.yandex.net https://yandex.ru 'self';
        connect-src https://api-maps.yandex.ru https://suggest-maps.yandex.ru https://*.maps.yandex.net https://yandex.ru;
        style-src blob:;

## v1 (начальные правила)

#### Правила
    Content-Security-Policy:
        img-src data: https://*.maps.yandex.net https://yandex.ru 'self';
        child-src https://api-maps.yandex.ru;
        frame-src https://api-maps.yandex.ru;
        script-src 'unsafe-eval' https://api-maps.yandex.ru https://suggest-maps.yandex.ru http://*.maps.yandex.net https://yandex.ru 'self';
        style-src blob:;
