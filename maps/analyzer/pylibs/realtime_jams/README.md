# Воспроизведение realtime пробок по проездам пользователей

## Пример

```python
from maps.analyzer.pylibs.realtime_jams.libs.build_jams import build_realtime_jams
import maps.analyzer.toolkit.lib as tk

with tk.get_context() as ytc:
    travel_times = tk.sources.fetch_jams_sources(ytc, "20210721", "20210721")
    jams = build_realtime_jams(ytc, travel_times)
```

## Описание алгоритма

См. [MAPSJAMS-3687](https://st.yandex-team.ru/MAPSJAMS-3687), также описано отличие от построения пробок в сервисе.
