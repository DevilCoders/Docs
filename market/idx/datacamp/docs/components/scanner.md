## Scanner
Микросервис, накатывающий данные из внешних источников в офферное хранилище.

## Настройки
- [TimestampFromTableName](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/scanner/etc/stocks_processors.cfg?rev=8268697&blame=true#L3) - вычисление таймстемпа данных по имени таблицы

## Скрытия офферов от ABO
прод - //home/market/production/abo/hiding_rule/blue_offer/recent
тестинг - //home/market/testing/abo/hiding_rule/blue_offer/recent

## Скрытия офферов от РАЗУМа
прод - //home/market/production/mbo/mboc/offer_hidings/recent
тестинг - //home/market/testing/mbo/mboc/offer_hidings/recent

## Статус публикации офферов (для посчета интегрального статуса)
прод - //home/market/production/indexer/datacamp/united/in/publication_status_diff/recent
тестинг - //home/market/testing/indexer/datacamp/united/in/publication_status_diff/recent

## Промоакции для синих
прод - //home/market/production/mbi/promo/potential_assortment/latest
тестинг - //home/market/testing/mbi/promo/potential_assortment_white/latest

## Промоакции для белых DBS офферов
прод - //home/market/production/mbi/promo/potential_assortment_white/latest
тестинг - //home/market/testing/mbi/promo/potential_assortment_white/latest

## Карточки модели (msku) от MBO
прод - //home/market/production/mbo/export/recent/models/sku
тестинг - //home/market/testing/mbo/export/recent/models/sku

