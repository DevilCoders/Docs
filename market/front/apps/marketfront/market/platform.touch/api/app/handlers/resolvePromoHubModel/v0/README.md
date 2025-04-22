### Хэндлер *resolvePromoHubModel*

Возвращает N количество акционных продуктов из категории, соответствующих определенной промо-механике.
Набор возвращаемых данных может содержать различные сущности  -  product или offer.

-Параметры
- `hid: integer | string | [integer] | [string]` - Необязательный параметр, определяет категорию, по которой будет произведен поиск продуктов
- `pageSize: integer` - Необязательный параметр (`default: 6`), определяет размер страницы выдачи.
- `page: integer` - Необязательный параметр (`default: 1`)
- `promo-type: [string]` - Необязательный параметр (`default: ['market']`), определяет промо-механику которая должна действовать на выбираемые продукты. Возможные значения элементов массива:
    - `'market'` - все промомеханики (`default`)
    - `'promo-code'` - промокоды
    - `'n-plus-m'` - при покупке N товаров получи M в подарок
    - `'gift-with-purchase'` - подарок при покупке товара
    - `'discount'` - скидка
- `clid: number` - id места показа ссылки на внешних ресурсах


## Ссылки на микроформаты данных

- `Offer` - https://github.yandex-team.ru/market/microformats/tree/master/offer
- `Product` - https://github.yandex-team.ru/market/microformats/tree/master/product
- `Shop` - https://github.yandex-team.ru/market/microformats/tree/master/shop
- `Vendor` - https://github.yandex-team.ru/market/microformats/tree/master/vendor
- `Category` - https://github.yandex-team.ru/market/microformats/tree/master/category
- `Picture` = https://github.yandex-team.ru/market/microformats/tree/master/picture
- `Navnode` - https://github.yandex-team.ru/market/microformats/tree/master/navnode
