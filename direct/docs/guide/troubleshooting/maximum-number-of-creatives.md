# Накопилось много креативов

## Подходящие ситуации

- в API / степах / веб-интерфейсе при добавлении объявлений возвращается ошибка про количество креативов
- в [светофоре](../../glossary/glossary.md#traffic-light) падает тест **UserObjectsCountTest** _"максимально допустимое количество креативов у <логин>"_

## Решение
Сначала проверить, не копятся ли на логине кампании.
Удалить лишние можно по соседней инструкции — [{#T}](maximum-number-of-campaigns.md).

Затем можно попробовать удалить креативы без привязки к объявлениям (в запрос подставить нужный ClientID):
```sql
DELETE bp FROM perf_creatives pc JOIN banners_performance bp USING(creative_id) LEFT JOIN campaigns c USING(cid) WHERE pc.ClientID = 6865906 AND creative_type = "performance"  AND c.cid IS NULL;
DELETE pc FROM perf_creatives pc LEFT JOIN banners_performance bp USING(creative_id) WHERE pc.ClientID = 6865906 AND creative_type = "performance" AND bp.creative_id IS NULL;
```
