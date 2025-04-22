
## Типы фидов
[Типы фидов](https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/newfeedtypes/)

Feed Type | Смысл в Едином Каталоге | Цвет фида
:--- | :--- | :---:
FEED_CLASS_SELECTIVE_BASIC_PATCH_UPDATE_SERVICE_PATCH_UPDATE | Ассортиментный аплоадный. Частичное обновление  | Белый & Синий
FEED_CLASS_SELECTIVE_BASIC_PATCH_UPDATE_SERVICE_FULL_COMPLETE | Ассортиментный аплоадный. Полное обновление | Белый & Синий
FEED_CLASS_SELECTIVE_BASIC_PATCH_UPDATE_SERVICE_FULL_COMPLETE | Ассортиментный по ссылке | Белый
FEED_CLASS_UPDATE | Ценовой аплоадный | Синий
FEED_CLASS_COMPLETE | Ценовой по ссылке | Синий
FEED_CLASS_STOCK | Стоковый | Синий
FEED_CLASS_ASSORTMENT_BASIC_PATCH_UPDATE_SALE_TERMS_SERVICE_FULL_COMPLETE | Ассортиментный аплоадный. Полное обновление, ошибки в базовой и сервисной частях не блокируют загрузку другой части | Белый & Синий

 ** Белый - ADV & DBS, Синий - FBx

## Траблшутинг)
[Траблшутинг заданий на парсинг](../support/offer.md#feed-trouble-shooting)

## Схема работы парсера фидов
Подробное описание [тут](../market/idx/datacamp/parser/README)

