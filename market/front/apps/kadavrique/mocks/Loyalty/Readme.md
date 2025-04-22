# Loyalty

Данные в стейте:

```
{
    "Loyalty.collections": {
        bonus: [
            bonusItem,
            ...
        ],
        promos: [
            promoItem,
            ...
        ],
        perks: [
            perkItem,
            ...
        ],
        promocodes: [
            promocodeItem,
            ...
        ],
        notification: {
            notificationGroups: ['YANDEX_PLUS'],
        },
        userCoupon: {
            [userId]: code,
        },
        userPromocode: {
            [userId]: ['code'],
        },
        userFreeDeliveryWelcomeBonusStatus: {
            promoStatus: 'REGISTRATION_ALLOWED'
                | 'REGISTRATION_NOT_ALLOWED'
                | 'REGION_NOT_ALLOWED'
                | 'PROMO_NOT_ACTIVE'
                | 'null',
            userStatus: 'REGISTERED'
                | 'NOT_REGISTERED',
        },
        freeDeliveryWelcomeBonusInfo: {
            minOrderTotal: number,
        }
        referralPromoCode: {
            // признак успешной генерации промокода
            isPromocodeAvailable: boolean,
            // промокод
            refererPromoCode: string,
            // срок годности промокода ZonedDateTime
            refererPromoCodeExpiredDate: string,
            // сколько кэшбэка ожидается (заказы ещё не получены)
            expectedCashback: number,
            // сколько друзей сделало заказ по промокоду
            friendsOrdered: number,
            // ссылка которую будем вставлять в текст собщения "поделяшки"
            refererLink: string,
            // сколько баллов уже получено по реферальной программе
            alreadyGot: number,
            // информация о партнёрской программе
            partnerProgramInfo: {
                partnerProgramMaxReward: ?number, //  максимальный размер вознаграждения который можно получить
                partnerProgramLink: string, // ссылка на страницу c описанием программы
            },
        },
        notifications: [
            notificationItem,
            ...
        ],
    },
}
```

## Ручки

### `/cart/coins`

Отдается весь список бонусов из `Loyalty.collections.bonus` с учетом состава корзины и сроком годности бонусов

**Дополнительные св-ва бонусов**
* через св-во restrictionSum задается ограничение по сумме для применение бонуса
* через св-во isNotProcessable задается техническая ошибка применение бонуса

Дополнительные св-ва вычищаются из бонусов перед отдачей списка бонусов

**Принятые допущения:**
* фильтрация бонусов в зависимости от состава корзины только для FIXED бонусов
* фильтрация бонусов в зависимости от состава корзины для FIXED бонусов только по ограничению на MSKU и по сумме заказа
* бонусы не привязываются к текущему пользователю, они доступны для всех.

### `/coins/orderStatusUpdated`

Отдается весь список бонусов из `Loyalty.collections.bonus`.

### `/coins/orderStatusUpdated`

Аналогичен `/coins/orderStatusUpdated`, только отдаётся еще и пустой список "старых" бонусов.

### `/promo/byCode`

Возвращает {id} промо-акции по ее коду или code: PROMO_NOT_FOUND, если акция не найдена

### `/promo/coin/<id>`

Возвращает указанную промо-акцию по ее id или код 404 и пустой ответ

### `/coins/bind`

Ищет в коллекции монету по ее activationToken. Если найдена - вовзращает ее, если нет - возвращает code: UNKNOWN_ERROR

### `/coins/getActiveCoinsCount`

Возвращает кол-во активных бонусов. Активные бонусы определяются по ряду признаков(поля status и endDate)

### `/coins/person`

Возвращает все бонусы, разделенные на coins и futureCoins

**Дополнительные св-ва бонусов**
поле бонуса isFuture задает в какое поле попадет бонус

### `/coins/coin`

возвращает запрошенный бонус или 404 и пустой ответ

### `/discount/priceLeftForFreeDelivery/v3`
и
### `/discount/priceLeftForFreeDelivery/v2`

Возвращают трешхолд доставки для товаров

### `/loyalty-programs/byUid/<uid>`

Возвращает промоакции в которых участвует пользователь

Пример ответа
```
{
    promos: [
        {
            endDate: '28-10-2019 14:30:19',
            promoType: 'SECRET_SALE',
            promoKey: '121212',
            startDate: '28-09-2019 14:30:19',
        },
    ],
}
```

### '/perk/status'

Возвращает список перков со статусами для указанных в параметре perkType типов перков

Пример ответа
```
{
    statuses: [
        {
            freeDelivery: true,
            orderId: 1,
            purchased: true,
            type: 'YANDEX_PLUS',
        },
    ],
}
```

### '/notifications/status'

Возвращает информацию о непросмотренных группах уведомлений

Пример ответа
```
{
    notificationGroups: ['YANDEX_PLUS'],
}
```

### '/notifications/markAsRead'

Помечает группы уведомлений как просмотренные (фильтрует массив notificationGroups в стейте)

Всегда возвращает `{status: "OK"}`

### /promo/byPromoGroupToken

Возвращает список бонусов, запрашиваемой промо-группы

В репозитории marketplace есть мок '@/spec/hermione/kadavr-mock/loyalty/efimFutureCoins.js'
Пример успешного ответа (промо-группа найдена)
```
{
    futureCoins: [
        {
            title: '',
            subtitle: 'на туалетную бумагу',
            coinType: 'FIXED',
            nominal: 5000.00,
            description: 'Туалетная бумага… много туалетной бумаги.',
            inactiveDescription: null,
            image: 'https://avatars.mdst.yandex.net/get-smart_shopping/69393/9f985f9b-42fa-47a1-8bc5-1db1c5fc9937/',
            images: {
                standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/69393/9f985f9b-42fa-47a1-8bc5-1db1c5fc9937/',
            },
            backgroundColor: '#49ff00',
            endDate: null,
            promoEndDate: '01-05-2020 20:00:00',
            outgoingLink: '/catalog/tualetnaia-bumaga-salfetki/80973/list',
            bindingStatus: {
                activationCode: 'source',
                reason: null,
                isAvailable: true,
            },
        },
    ],
}
```
При ответе с ошибкой, на фронте ожидаются code, message, statusCode
В репозитории marketplace можно глянуть тут: @/resources/loyalty/errors.js

Ошибки ожидаются в коллекции loyaltyErrors

На фронте пробрасывать так:
```
await this.browser.setState(
        'Loyalty.collections.loyaltyErrors',
        {
            getFutureBonusesByPromoGroupToken: {
                code: 'errorCode',
                message: 'errorMessage',
                statusCode: 404, // errorStatusCode (number)
            },
        }
    );
```

Если не проброшено ни одиного, мока вернется дефолтная ошибка
```
statusCode = 404;
code: 'UNKNOWN_ERROR',
message: 'SOMETHING_WRONG',
```

### /coins/createCoin/v2

Возвращает привязанную пользователем монетку, или ошибку при привязке

Для создание монетки, необходимо пробросить мок в bindedBonusCollection коллекцию кадавра
В репозитории marketplace есть мок '@/spec/hermione/kadavr-mock/loyalty/bindedBonus.js'

Пример ответа с успешной привязкой
```
{
    id: 1,
    title: 'Скидка 1%',
    subtitle: 'на коронавирус',
    coinType: 'PERCENT',
    nominal: 1,
    description: 'Отличный способ заразится коронавирусом! +1% к шансу заражения',
    inactiveDescription: null,
    creationDate: '01-05-2020 20:00:00',
    endDate: '01-05-2020 20:00:00',
    image: 'https://avatars.mdst.yandex.net/get-smart_shopping/69393/0c17297e-8987-4652-98a3-3b861b20d790/',
    images: {
        standard: 'https://avatars.mdst.yandex.net/get-smart_shopping/69393/0c17297e-8987-4652-98a3-3b861b20d790/'
    },
    backgroundColor: '#49ff00',
    status: 'ACTIVE',
    requireAuth: false,
    activationToken: null,
    coinRestrictions: [{restrictionType: 'CATEGORY', msku: null, categoryId: 91491}],
    reason: 'OTHER',
    reasonParam: null,
    shortTerm: false,
    bonusLink: null,
    outgoingLink: null,
    isCategoryBonus: true,
};
```

При ответе с ошибкой, на фронте ожидаются code, message, statusCode
В репозитории marketplace можно глянуть тут: @/resources/loyalty/errors.js

Ошибки ожидаются в коллекции loyaltyErrors

На фронте пробрасывать так:
```
await this.browser.setState(
        'Loyalty.collections.loyaltyErrors',
        {
            createBonusByPromoId: {
                code: 'errorCode',
                message: 'errorMessage',
                statusCode: 404, // errorStatusCode (number)
            },
        }
    );
```

Если не проброшено ни одиного мока, вернется дефолтная ошибка
```
statusCode = 404;
code: 'UNKNOWN_ERROR',
message: 'SOMETHING_WRONG',
```

### `/promocodes/referral/get/<uid>`

Возвращает реферальный промокод для пользователя

Пример ответа
```
{
    isPromocodeAvailable: true,
    refererPromoCode: "PROMOCODE",
    refererPromoCodeExpiredDate: "2021-08-09T20:59:59Z",
    expectedCashback: 900,
    friendsOrdered: 2,
    alreadyGot: 600,
    refererLink: "https://market.yandex.ru/?utm_source=market&utm_medium=link&utm_content=referral_friend_link",
    partnerProgramInfo: {
        partnerProgramMaxReward: 50000,
        partnerProgramLink: "https://aff.market.yandex.ru/influencers",
    },
}
```

### `/notifications/current`

Возвращает список не прочитанных уведомлений пользователя

Пример ответа
```
[
  {
    "id": "120",
    "type": "REFERRAL_ACCRUAL",
    "link": "https://market.yandex.ru/deals?utm_source=market&utm_medium=banner&utm_campaign=MSCAMP-77utm_term=src_market&utm_content=referal_touch_popup",
    "img": "https://avatars.mds.yandex.net/get-smart_shopping/1396237/e794f67f-7e9d-4587-9950-6c6dbf67957b/orig",
    "message": {
      "title": "Вам 300 баллов за друга",
      "text": "Потратьте их на что-нибудь",
      "linkLabel": "За покупками"
    },
    "params": {
      "amount": "300",
      "is_plus": "true",
      "count": "3"
    },
    "dlink": ""
  }
]
```

### `/notifications/accept`

Помечает уведомления как просмотренные

Всегда возвращает `{status: "OK"}`
