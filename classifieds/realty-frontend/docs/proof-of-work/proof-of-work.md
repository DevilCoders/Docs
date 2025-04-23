# Proof of work
## Что это
Способ проверить, что гейт используется клиентом-браузером, а не примитивным парсером.

В частности, используется для защиты от парсинга номеров телефонов на сайте недвижимости.

## Принцип работы
Сервер использует соль и переданный с клиента payload (параметры запроса), чтобы создать одноразовый nonce-ключ.
Этот nonce передаётся на клиент, который должен потратить ресурсы на то, чтобы превратить nonce в hash с помощью определённого алгоритма.

После этого, клиент отправляет hash, nonce и payload на сервер вместе с запросом (например, телефона), где сервер проверяет что hash
действительно может быть вычислен с помощью данного nonce, и, в случае успеха, выполняет оригинальный запрос (телефона).

Соль нужна для того, чтобы быстро проверить правильность hash вместо повторного его вычисления (см. [графики сложности вычисления/проверки](https://github.com/indutny/proof-of-work#complexity))

![sequence](pow-sequence.png)

[Больше информации об используемой для шифрования/вычисления библиотеке](https://github.com/indutny/proof-of-work)

## Реализация в коде
Pow в недвижимости построен на npm-библиотеке [`@vertis/proof-of-work`](https://github.com/YandexClassifieds/vertis-frontend/tree/main/packages/proof-of-work). Она также используется auto.ru.

Работа с библиотекой реализована внутри `Gate`, как [клиентского](../../realty-core/view/react/libs/gate.js), так и серверного. Функционал pow подключается к серверному `Gate` через [миксин](../../realty-core/app/controller/mixin/gate_pow_check.js).

Получение `nonce` происходит внутри отдельного гейта: [`proof-of-work`](../../realty-core/app/controller/gates/proof-of-work.js). Обращение к этому гейту происходит когда клиент отправляет параметр `usePow` вместе с запросом в какой-либо гейт.

## Как добавить вычисление и проверку pow к гейту
1. Подключить миксин к гейту на nodejs:
```js
    // app/controller/gates/myGate.js
    const Gate = require('./gate');
    const PowCheckMixin = require('realty-core/app/controller/mixin/gate_pow_check');

    const MyGate = Gate.create();

    MyGate.mixin(PowCheckMixin); // <--------------
```

2. Добавить нужным экшнам этого гейта параметр `requireProofOfWork: true`:
```js
    // app/controller/gates/myGate.js
    MyGate
        .action({
            name: 'myAction',
            requireProofOfWork: true, // <--------------
            fn() {
                // do what action needs to do
            }
        })
```

1. При запросе к гейту __с клиента__ отправлять дополнительный параметр `usePow`, тогда параметры запроса будут использоваться для изначального создания `nonce`:
```ts
    import Gate from 'realty-core/view/react/libs/gate';

    const getSomethingFromServer = async (offer: IOfferCard) => {
        const { offerId } = offer;

        const something = await Gate.get(
            'myGate.myAction',
            { id: offerId },
            { usePow: true } // <--------------
        );

        // ...
    }
```

Пример реализации можно посмотреть для гейта получения номера телефона оффера: [гейт на nodejs](../../realty-core/app/controller/gates/offer-phones.js), [обращение к гейту на клиенте](../../realty-core/view/react/modules/offer-phones/actions.ts).

## Полезное
Соль для создания хэша в секретнице: https://yav.yandex-team.ru/secret/sec-01fbp7js3zv2ns59kpzgk2k0zw/explore/versions
