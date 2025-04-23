# giftPromoTimeout
**Type:** Int Long Long
**Default:** 3 604800000 (7 дней) 3600000 (1 час)

**Related tickets**
[TVANDROID-5194](https://st.yandex-team.ru/TVANDROID-5194)

**Context**
```json
{
  "com.yandex.tv.services": {
    "giftPromoMaxCount": "count",
    "giftPromoTimeout": "ms",
    "giftPromoLackTtl": "ms"
  }
}
```

**Description**
Пока нет бекенда для промиков, логика показа промо подарка сделана на клиенте. 
Параметры показа промо подарка:
- `giftPromoMaxCount` - максимальное количество показов промо подарка на устройство,
- `giftPromoTimeout` -  минимальный таймаут между показами,
- `giftPromoLackTtl` - через сколько вновь идем за подарком на бекенд, если его не было для этого устройства.


