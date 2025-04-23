# Изменения рефералки такси. Разделение по брендам

## Общие положения

### Сейчас

1. Нет разделения реферальных кампаний по брендам
2. Бренды yataxi и yango проставлены промокодам в таблице referral.promocodes
3. __/referral__, __/shortcuts__ могут вернуть рефералки брендов, отличных от бренда приложения пользователя
4. __/couponactivate__, __/couponcheck__, __/couponreserve__ позволяют обрабатывать промокод одного бренда в приложении другого 

### Новое

1. Реферальные кампании разделены по брендам
2. В таблицу referral.campaigns добавляется бренд как свойство кампании, заменяя тем самым бренд в referral.promocodes
3. __/referral__, __/shortcuts__  не могут вернуть рефералки брендов, отличных от бренда приложения пользователя
4. __/couponactivate__, __/couponcheck__, __/couponreserve__ не позволяют обрабатывать промокод одного бренда в приложении другого 

### Как бренды yango и yataxi используются в странах
#### Как должно быть:
- **yango**: Финляндия, Гана, Кот-д'Ивуар, Израиль, Румыния
- **yataxi**: остальные страны
- т.о. одновременно оба бренда не используются в одной стране

#### Какие несоответствия есть в базе

Бренд yataxi в странах бренда yango
```
select country, count(*) from referral.promocodes where brand_name='yataxi' and country in ('fin', 'gha', 'ci', 'isr', 'rou') group by country;
 country | count |  total  
---------+-------+---------
 fin     |  3637 |  66588
 gha     |   222 |  90412
 isr     |  7903 | 211810
 rou     |  1501 | 145182
```

Бренд yango в странах бренда yataxi
```
select country, count(*) from referral.promocodes where brand_name='yango' and country not in ('fin', 'gha', 'ci', 'isr', 'rou') group by country;
 country | count |  total  
---------+-------+---------
 blr     |   353 |  953434
 est     |  2268 |  120603
 geo     |  1875 |  483234
 kaz     |    71 | 1063495
 kgz     |   117 |  608855
 ltu     |   158 |   56161
 lva     |   585 |  197835
 mda     |  1055 |  267117
 rus     |    19 |   36522
```

Итого расхождения в каждой из стран не превышают 6% от общего числа реферальных промокодов.

В промокодах с несоответствиями бренд будет изменён на бренд, соответствующий стране. При этом, например, в Финляндии, стране бренда yango, перестанет действовать рефералка у пользователей yataxi. При обращении в поддержку по поводу исчезновения рефералки - нужно просить установить другое приложение.

Пустые brand_name
```
select brand_name, count(*) from referral.promocodes group by brand_name;
 brand_name |  count  
------------+---------
 yango      |  475094
 yataxi     | 3684419
            |  141433
```

Сколько промокодов бренда yango с пустым brand_name
```
select country, count(*) from referral.promocodes where brand_name is null and country in ('fin', 'gha', 'ci', 'isr', 'rou') group by country;
 country | count 
---------+-------
 fin     |  3301
 isr     | 14903
 rou     | 13887
```

### Порядок изменений в базе и в коде
1. [миграция-1] добавить колонку brand_name в referral.campaigns
2. [код-1] IsCampaignEnabled возвращает true для campaign_name "common_yango"
3. [вручную-1] добавить "brand_name":"yango" и "extra_campaign":"common_yango" в нужные элементы конфига REFERRAL_CREATOR_CONFIG (с зонами и странами бренда yango)
4. [скрипт-1] доработать и запустить скрипт [sync_with_creator_config.py](https://github.yandex-team.ru/taxi/tools-py3/blob/master/taxi_coupons/sync_with_creator_config.py) для синхронизации таблиц referral.campaigns и referral.creator_configs и конфига REFERRAL_CREATOR_CONFIG 
5. [вручную-2] добавить "extra_campaign":"common_yango" в нужные элементы конфига REFERRAL_CONSUMER_CONFIG. Добавлять brand_name нет необходимости, т.к. имя кампании однозначно его определяет.
6. [скрипт-2] проапдейтить campaign_id в referral.promocodes через [fix_referral_campaigns_ids.py](https://github.yandex-team.ru/taxi/tools-py3/blob/master/taxi_coupons/onetime/fix_referral_campaigns_ids.py)
7. [код-2] перестать использовать колонку brand_name из referral.promocodes. Переключиться на campaign.brand_name
8. [миграция-2] удалить колонку brand_name из referral.promocodes
9. [код-3] фильтрация по бренду в __/referral__, __/shortcuts__, __/couponactivate__, __/couponcheck__, __/couponreserve__
10. [вручную-3] ограничиться брендами yataxi и yango в эксперименте [grocery_referral_inside_taxi](https://tariff-editor.taxi.yandex-team.ru/experiments3/show/grocery_referral_inside_taxi)
11. [вручную-4] убедиться, что серии промокодов для Убера содержат платформы, иначе не пройдёт [проверка](https://github.yandex-team.ru/taxi/uservices/blob/af53c4368d3f5d2be331fa09d1f4a86e47d2c361/services/coupons/src/couponcheck/checks/checks.cpp#L237)
