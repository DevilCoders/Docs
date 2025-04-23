# easyview pylib

Библиотека для вывода easyview-объектов.<br>
См. пример использования в [`examples/draw_py`](/arc/trunk/arcadia/maps/tools/easyview/examples/draw_py):
```bash
./examples/draw_py/draw_py | ./bin/easyview
```

```python
import maps.tools.easyview.pylib.draw as ev


def output():
    return ev.point(
        data={
            'value': 10,
            'str': 'lala',
        },
        lon=55.0,
        lat=33.0,
        style=ev.pointstyle(
            fill=ev.rgba(1.0, 0.0, 0.0),
            outline=ev.rgba(0.0, 1.0, 0.0),
            size=3,
        ),
        animation=ev.animation(
            since=10, until=20,
            focus=False, balloon=False,
        ),
    )
```
