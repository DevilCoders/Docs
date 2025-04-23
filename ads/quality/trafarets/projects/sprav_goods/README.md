# Трафареты с ресурсами справочника

## Goods and prices

### Исходные данные

Banner (pk:BannerID, ...)
//home/??

BannerToText (pk:BannerID, ...)
//?

BannerPhrase
//?

BannersToPermalink (pk: BannerID + permalink, score, backa_rubricks)
Автоматическая привязка пермалинков к баннерам
//home/altay/y-direct/current-state/banners-to-permalink
- Что такое score? Надо ли ставить порог на score?

Таблица директа с маппингом баннеров на пермалинки
"//home/direct/mysql-sync/current/ppc:CAST($index AS String)/straight/banner_permalinks";
- Кто варит эту табличку
- Что такое uniq_cond (похоже на битовую маску)
- Есть permalink_assign_type и там "auto/manual". Что делать с ручной привязкой (приоритет над автоматической?)

GoodsAndPrices
Таблица товаров по пермалинкам
//home/sprav/goods_and_prices/db/raw_data
- Proto-схема arcadia/sprav/goods_and_services/funduk/core/proto/model.proto#L22
- Нет уникального идентификатора товара. Можно добавить?
- Что такое category (текстовая)? Может быть есть category_id?
- name - название карточки товара - required
- price - цена - optional


### Привязка
Фильтрация баннеров:
- Только активные баннеры?

Фильтрация карточек товаров:
- Убрать очевидно плохо-заполненные

Итоговый джойн
Join(
    Banner,
    BannerToText,
    BannerToPermalink,
    GoodsAndPrices
)

Применить прогнозатор для вычисления relevance карточки к баннеру

Отфильтровать по порогу на relevance

Для каждого баннера отбираем галерею по условию:
- Num(goods) >= 3
- Num(photo_link is not None) >= 3
- Num(desciption is not None) >= 3

Как устроен выходной формат:
{Banner, permalink, ??}

