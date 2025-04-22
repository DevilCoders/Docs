# CouponsCarousel - Карусель купонов

## Данные

+ **promoGroupToken** - Идентификатор группы акций (смотреть в Админке лоялти)
+ **couponSize** - Размер купонов (см. [CoinBase](https://github.yandex-team.ru/market/marketfront/blob/master/src/uikit/components/CoinBase))
+ **carouselTitle** - Заголовк карусели, не обязательный параметр
+ **carouselSubtitle** - Подзаголовок карусели, не обязательный параметр

## Вьюха

[Вьюха](https://disk.yandex.ru/public/nda/?hash=bJK2TRzVt2FRNgPFHivW06cDatpk7MxJNcTxRsu55AXNCVGkQal1MJgfja4nsJdlq/J6bpmRyOJonT3VoXnDag%3D%3D)


## Как заводить

1. В админке лоялти создается новая группа акций
2. В CMS подключаем виджет "Карусель купонов" на страницу с нужными параметрами и promoGroupToken и promoGroupType из админки

## Как работает

Работает по принципу [ЕФИМа](https://wiki.yandex-team.ru/market/pokupka/projects/users-2019/kontur-ltv/dev/efim-2.0/)

Пользователь может забирать купоны из карусели. Карусель имеет два состояния:

1. [Если пользователь уже забрал хоть один купон, добавляется ссылка в колекцию бонусов](https://disk.yandex.ru/i/Lonf3Zvq90xcFQ)

2. [Если пользователь забрал все купоны](https://disk.yandex.ru/i/YGFyF3rz7oF37A)

Также есть скрытая возможность с подпиской пользователя на плюс, включаетяс через s3 фичтогл, но для использования необходимо получить токены от Плюса
