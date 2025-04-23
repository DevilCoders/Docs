## Как устроены тесты cargo-dispatch

### Happy path

#### Сущности

- 5 сегмента: seg1, seg2, seg3, seg5, seg6.
  - seg1 с мультиточками.
  - seg5 и seg6 - сегменты без маршрутных листов, идентичны seg1 и seg2
- 2 роутера: smart-enough-router, fallback-router.
  - smart-enough-router получает только seg1 и seg2.
- 4 маршрутных листов:
  - 3 строит фолбечный роутер: `waybill_fb_<1, 2, 3>` для
    сегментов 1-1.
  - 1 строит умный роутер: `waybill_smart_1`, склеивая seg1 и seg2.
  - Выигрывают `waybill_smart_1` и `waybill_fb_3`.


#### Статика

Эксперименты 3.0:
- 'segment_routers' для назначения роутеров.

Ответы ручки журнала репликации сегментов из claims:
- `claims_segment_journal__1__new_segments.json`
  - Первые упоминания о сегментах.


### Фикстуры

Эксперименты 3.0:
- `happy_path_exp3` устанавливает эксперименты `happy_path/exp3*.json`.

Стейты:
- `happy_path_state_new_segments` реплицирует новые сегменты.
- `happy_path_state_new_segments_with_routers` дополнительно регистрирует участвующие роутеры.
