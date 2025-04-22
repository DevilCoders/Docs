## Детская вертикаль
https://st.yandex-team.ru/TAXIPROJECTS-1151

## MVP
Объединение категорий в которых есть *новое* детское кресло childchair_v2

## zoneinfo API

```
"verticals": [
    {
      "title": "Детский",
      "type": "group",
      "can_make_order_from_summary": false,
      "tariffs": [ ... ],
      // новые поля
      "requirement_overrides": [
        {
          "name": "childchair_v2",                  // required
          "glued": true,                            // optional
          "optional_glued": false,                  // optional
          "unset_order_button": "Выбрать кресло"    // optional
        }
      ]
    }
  ]
```
