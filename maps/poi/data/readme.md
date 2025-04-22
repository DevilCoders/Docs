# `poi/data`

Содержит в себе полезные константы и прочую информацию про пои.

### `zoom_conflict_meters.json`

Расстояния в метрах, используемые для вычисления зума конфлита двух поев.
Это очень грубая их оценка и по сути очень неточная. По возможности используй
`precise_zoom_conflict_meters.json`

### `precise_zoom_conflict_mercator_distance.json`

Расстояния в меркаторных единицах (или в метрах на экваторе), используемые для вычисления
зума конфлита двух поев, но в отличие от `zoom_conflict_meters.json` точнее. В файле содержатся
расстояния для четырех случаев:
1. Конфликт негеопродута с негеопродуктом `poi_vs_poi` (`px_distance = 28`)
2. Конфликт геопродукта с геопродуктом `gp_vs_gp` (`px_distance = 32`).
3. Конфликт геопродукта с негеопродуктом `gp_vs_poi` (`px_distance = 44`).
4. Старые расстояния из `zoom_conflict_meters.json` пересчитанные в меркаторных единицах `old`.

*(о том, откуда тут два случая и такие значения `px_distance`, можно прочитать вот в
[этом тикете](https://st.yandex-team.ru/GEOQ-416#5fae662fe3cc041f2d2ac4e9))*

Для вычисления расстояний использовался простой брутфорс

```python
from itertools import product

import numpy as np

from yandex.maps import tileutils5 as tu
from yandex.maps.geolib3 import (
    Point2, geo_to_mercator, geodistance
)


def geo2pixel(lon, lat):
    mercator_coord = geo_to_mercator(
        Point2(float(lon), float(lat)))
    pixel_coord = tu.TiePoint(
        tu.RealCoord(mercator_coord.x, mercator_coord.y)).pixel()
    return pixel_coord.x(), pixel_coord.y()


def search_threshold(pos: np.ndarray, zoom: int, px_distance: int):
    pos_pixel = np.array(geo2pixel(*pos)) >> (23 - zoom)

    for x_d, y_d in product(np.arange(0.0, 1e-3, 1e-6), repeat=2):
        new_pos = np.array((pos[0] + x_d, pos[1] + y_d))
        new_pos_pixel = np.array(geo2pixel(*new_pos)) >> (23 - zoom)

        if int(np.linalg.norm(pos_pixel - new_pos_pixel)) == px_distance:
            yield geodistance(Point2(*pos), Point2(*new_pos))
```

Чтобы получить пороговое значение на интересующей тебя широте, достаточно значение порога
домножить на `math.cos(math.radians(lat))`.

### `validation_zoom_conflict_meters.json`

Расстояния в метрах для медианной широты геопродукта, которая на момент расчета равнялась
`55.520927932934924`. Получены таким же методом, что и `precise_zoom_conflict_mercator_distance.json`
для `px_distance = 32`.

### `rubric_info.json`

Содержит информацию про рубрики из Алтая.
