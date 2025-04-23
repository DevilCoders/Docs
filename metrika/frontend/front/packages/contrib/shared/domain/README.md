# Services

> Памятка при добавлении сервиса

## Поле `domain`

Домен для сервиса

## Регион

Регион высчитывается исходя из языка сайта Метрики. Для каждого языка он свой.

## Поле `tlds`

Это маппинг региона к Top Level Domain (TLD) либо `true` если TLD будет всегда такой же как и в данный момент на сайте метрики.
См. пример ниже.

__Важно:__ при значении `true` TLD будет меняться только при изменении TLD на сайте метрики, _не_ при изменении языка,
то есть при значении `tlds: true` если на сайте `https://metrika.ru` выставлен английский язык например, то ссылка все равно
будет вести на `.ru` несмотря на язык, так как на сайте метрики TLD равен `ru`.

Также можно выставить `tlds: false`, тогда вместо TLD будет приклеиваться пустая строка `''`. Удобно если TLD везде одинаковый.

## Поле `path`

Путь для сайта.

## Поле `pathFromTld`

Это маппинг финального TLD (который высчитывается из поля `tlds`) к пути для сайта, нужен если используется разный путь для
разных TLD.

## Поле `pathFromRegion`

Это маппинг для пути сайта исходя из региона. Это поле будет использовано только если не задано поле `pathFromTld` и поле `path`.

## Примеры

1.
    ```js
    const services = {
        promo: {
            domain: 'yandex.',
            tlds: {
                ru: 'ru',
                com: 'com',
                tr: 'com.tr',
            },
            path: '/promo/freeservice/metrica',
        },
    }
    ```

    Для русского региона будет `//yandex.ru/promo/freeservice/metrica`, для англоязычного -
    `//yandex.com/promo/freeservice/metrica`, для турецкого - `//yandex.com.tr/promo/freeservice/metrica`.
2.
    ```js
    const services = {
        blog: {
            domain: 'yandex.',
            tlds: {
                ru: 'ru',
                com: 'com',
                tr: 'com',
            },
            pathFromTld: {
                ru: '/blog/metrika',
                com: '/blog/metrica',
            },
        },
    }
    ```

    Для русского региона будет `//yandex.ru/blog/metrika`, для англоязычного и турецкого - `//yandex.com/promo/freeservice/metrica`.

3.
    ```js
    const services = {
        passport: {
            domain: 'passport.yandex.',
            tlds: true,
        },
    };
    ```

    Для русского региона будет `//passport.yandex.ru`, для англоязычного - `passport.yandex.com`, для турецкого -
    `//passport.yandex.com.tr`. Так как маппинг региона к TLD на сайте метрики `ru -> ru`, `en -> com`, `tr -> com.tr`.
