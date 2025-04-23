# easyview lib

include: `include/io.h`

В [`include/format/yson.h`](include/format/yson.h) лежат вспомогательные функции для упрощения вывода стилей, анимации и некоторой геометрии в yson формате.

Пример:
```cpp
#include <maps/tools/easyview/lib/include/io.h>

namespace ev = maps::tools::easyview;

NYT::TNode out = NYT::TNode::CreateMap()
    ("value", 10)
    ("str", "lala")
    ("lon", 55.0)
    ("lat", 33.0)
    (ev::yson::POINTSTYLE, ev::yson::pointStyle(
        Color::rgba(1.0, 0.0, 0.0),
        Color::rgba(0.0, 1.0, 0.0),
        3
    ))
    (ev::yson::ANIMATION, ev::yson::animation(
        10, 20, false, false
    ));
```
