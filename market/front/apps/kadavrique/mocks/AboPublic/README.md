# AboPublic
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html).

Данные в стейте:

```
{
    shopBadUrls: {
        shopId: 10203104,
        badUrls: [
            {
                offline: false,
                online: false,
                finishedTime: '2018-12-19T16:46:56.884Z',
                url: 'https://www.ozon.ru/context',
                httpStatus: '404',
            },
        ],
    },
    shopAnswerStat: {
        shopId: 10203104,
        stat: {
            minAnswerTime: 0,
            maxAnswerTime: 21072,
            avgAnswerTime: 116,
            offTime: 1300,
            offCount: 1000,
        },
    },
}
```

## runOrderCheck
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/check-order-controller/runCheckOrderUsingPOST)

Запускает контрольный заказ.

## getLastBadUrls
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#!/url45checker45controller/getLastBadUrlsUsingGET).

Возвращает ровно то, что передали (данные в JSON формате)
Массив данных по проблемным урлам конкретного магазина или пустой массив.


## getShopAnswerStat
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#!/url45checker45controller/getShopAnswerStatUsingGET).

Возвращает ровно то, что передали (данные в JSON формате)
Статистику по простою магазина, если она есть, иначе - null.

## getProblems
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/partner-problem-controller/getShopProblemsUsingGET_1).

Возвращает ровно то, что передали (данные в JSON формате)
Проблемы магазина, если они есть, иначе - null.

## getOrderLimit
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/cpa-controller/getOrderLimitUsingGET).

Возвращает ровно то, что передали (данные в JSON формате)
Ограничение на количество заказов поставщика, если они есть.

## getPartnerRating
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/cpa-controller/getPartnerRatingUsingGET).

Возвращает ровно то, что передали (данные в JSON формате)
Рейтинг поставщика.

## getOgrnInfo
[Документация](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/spark-controller/getOgrnInfoUsingGET).

Просто возвращает данные из поля response из state (данные в JSON формате)
Информация о организации по ИНН/ОГРН.