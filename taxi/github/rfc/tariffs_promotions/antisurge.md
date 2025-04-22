## Задача
Перенести антисурж предложение в промопшлашку

## Дизайн
Сейчас это выглядит так
![Старый антисурж](img/antisurge_old.jpg)

## Механика

Предложение по антисуржу формируется в `routestats` как альтернативный оффер с `"type": "explicit_antisurge"`.

## Механика для промоплашек

В запрос api inapp-communications добавляем поле `alternative_offers`:

```
+   AlternativeOffer:
+       type: object
+       properties:
+           offer_id:
+               type: string
+           type:
+               type: string
+       required:
+         - offer_id
+         - type
+       additionalProperties: false

    SummaryState:
        type: object
        properties:
            offer_id:
                type: string
+           alternative_offers:
+               type: array
+               items:
+                   $ref: '#/definitions/AlternativeOffer'
            tariff_classes:
                type: array
                items:
                    type: string
        required:
          - tariff_classes
+         - alternative_offers
        additionalProperties: false
```

Далее  поле пробрасываем в новый source, который будет сделан отедельной ручкой
в `tariffs-promotions`.

В `tariffs-promotions` по `AlternativeOffer.type = explicit_antisurge` будем ходить в сервис
`order-offers` за оффером, и уже на основе офера формировать контент для промоплашки.

Шаблон для промоплашки будет браться из кэш-компоненты promo_block_cache_component.

Фолбэк: если не удалось получить оффер, то отдаем пустой список промоплашек.
Тайминги ожидаются как у ручки `/tariffs-promotions/v1/promotions`

Нагрузка: посколько предложения антисуржа является редким, то нагрузка на order-offers должна остаться в пределах +/- 5% 