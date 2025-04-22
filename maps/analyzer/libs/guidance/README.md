Библиотека для ведения по маршруту.
===

На вход получает сигналы и выставляемый в процессе движения маршрут, на выходе возможные события вида "ушли с маршрута"/"вернулись на маршрут"/"доехали до финиша" и местоположение автомобиля.
Примечаение: возможна ситуация, когда события "ушли с маршрута" не было — т.е. считается, что мы всё ещё на нём — однако лучшее местоположение не на маршруте. Уход с маршрута — весомое событие, которое не генерируется сразу, как только на это возникло подозрение.

Значимые изменения стоит отражать в [changelog](changelog), из которого при сборке читается версия. Так затем проще отлаживаться, так как версия логируется.

Пример использования
===
```cpp
#include <maps/analyzer/libs/guidance/include/config.h>
#include <maps/analyzer/libs/guidance/include/config/storage.h>
#include <maps/analyzer/libs/guidance/include/guide.h>
#include <maps/analyzer/libs/guidance/include/graph/compact_graph.h>
#include <maps/analyzer/libs/guidance/include/route/segments_route.h>

using namespace maps::analyzer::guidance;
namespage geo = maps::analyzer::external::geo;

int main() {
    Config cfg = defaultConfig;
    readConfig(&cfg, config::Node::fromFile("config.yaml"));

    Guide<RoadGraph, SegmentsRoute> guide{
        &cfg,
        fromGraph(...) // maps graph
        // also can specify starting route, or use `guide.setRoute` to update route
    };

    for (...) {
        // get signal from somewhere
        Signal signal = ...;
        const auto state = guide(signal);
        if (state.event) {
            // some event generated: `Lost`/`Finished`/`Returned`
            std::cout << "route event: " << *state.event << std::endl;
        }
        if (state.sequence) {
            // returned location
            const auto pt = RoadGraph::position(state.sequence.location.graphPoint);
            std::cout << "lon=" << geo::lon(pt) << "; lat=" << geo::lat(pt) << std::endl;
        }
    }
}
```

Описание API
===

- [`guide.h`](include/guide.h) — основной класс, `Guide`. Инициализируется указателем на конфиг (`nullptr` для использования дефолтного), графом и, опционально, маршрутом, который также можно менять по ходу.
- [`config.h`](include/config.h) — конфиг, представляет собой простую структуру. Есть дефолтный конфиг `defaultConfig`, а также функция чтения `readConfig`. Для загрузки стоит подключить [`maps/analyzer/libs/guidance/include/config/storage.h`](include/config/storage.h) и использовать соответствующие функции: `Node::fromFile`/`Node::fromString` в Аркадии, `JsonDocument::fromFile`/`JsonDocument::fromString` в Mapkit'е.
- [`config/storage.h`](include/config/storage.h) — базовый класс для хранилища конфигов и функции загрузки
- [`graph.h`](include/graph.h)/[`route.h`](include/route.h) — шаблонные классы для графа/маршрута, описывают необходимый интерфейс, который ожидают остальные классы от своих шаблонных параметров `Graph` и `Route`. Реализация предоставляется через специализацию методов для конкретных типов. См. например [`impl/internal/maps/graph.h`](impl/internal/maps/graph.h) и [`impl/internal/maps/route.h`](impl/internal/maps/route.h).
- [`debug.h`](include/debug.h) — получение отладочной информации, выставляется функцией `Guide::setDebug`
- [`types.h`](include/types.h) — используемые типы (сигналы, точки на графе, результирующее состояние и т.п.), простые структуры с данными
- [`graph/compact_graph.h`](include/graph/compact_graph.h) — реализация графа на основе `maps::road_graph`, класс `RoadGraph`. Только в Аркадии
- [`graph/road_graph.h`](include/graph/road_graph.h) — реализация графа на основе `RoadGraph` in Мапкитового `guidance`, класс `RoadGraph`. Только в Мапките.
- [`route/segments_route.h`](include/route/segments_route.h) — реализация маршрута как последовательности сегментов, класс `SegmentsRoute`. Только в Аркадии.
- [`route/indexed_route.h`](include/route/indexed_route.h) — реализация маршрута на основе `IndexedRoute` из Мапкита, класс `IndexedRoute`. Только в Мапките.

Описание реализации
===

Привязка проходит так:
1. Сначала сигнал привязывается к графу (`Binder` из [`impl/binder.h`](impl/binder.h)), в результате получаем `BoundPair` — два лучших кандидата (если они есть): на маршруте и не на маршруте.
2. Затем эта пара передаётся в три почти независимых класса, каждый из который выбирает, какой из двух кандидатов лучший
    * `Tracker` ([`impl/tracker.h`](impl/tracker.h)) — предпочитает маршрутный кандидат, т.е. даёт ему лишний вес, логика тривиальная
    * `FairTracker` ([`impl/fair_tracker.h`](impl/fair_tracker.h)) — выбирает наиболее весомый кандидат, таким образом реализуя т.н. "честную стрелку" — честное положение водителя. Однако для исключения ситуации, когда решение часто меняется (то на маршруте, то не на нём), используются некие эвристики.
    * `Clinger` ([`impl/clinger.h`](impl/clinger.h)) — реализует "прилипание" к маршруту: если мы ушли недостаточно далеко от маршрута, то считаем, что мы всё ещё на нём. Помимо `BoundPair` использует результат `Tracker`.
3. Затем на основе всех этих данных `Decider` ([`impl/decider.h`](impl/decider.h)) принимает окончательное решение, где находится водитель, а также поменялось ли маршрутное состояние.
