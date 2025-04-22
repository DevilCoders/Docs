# Парсинг даты и времени

Простая библиотека для парсинга даты-времени или интервала. Принимает строку и строку формата или `NYT::TNode` и формат времени в ноде (`TimeType`), под капотом использует `std::get_time` и `std::put_time`, но помимо этого также:
* парсит и сериализует дробную часть секунд
* парсит оффсет таймзоны

Помимо этого есть функции для конвертации:
* результата из и в `std::time_t` — `toTimeT` и `fromTimeT`
* в различные представления даты/времени на YT:
    * `Date` (представлено кол-вом дней с unix-эпохи) — `yt::toDate`/`yt::fromDate`
    * `Datetime` (представлено кол-вом секунд с unix-эпохи) — `yt::toDatetime`/`yt::fromDatetime`
    * `Timestamp` (представлено кол-вом микросекунд с unix-эпохи) — `yt::toTimestamp`/`yt::fromTimestamp`
    * `Interval` (представлено микросекундами) — `yt::toInterval`/`yt::fromInterval`
* в и из `NYT::TNode` при спецификации формата времени в ноде (см. `TimeType`).

Также для `TimeType` есть функции конвертации из строки в енум и наоборот. (см `maps/libs/enum_io`).

Основные семейства функций:
* `parseTime` — парсит время. Если формат явно не указан, парсит в любом из основных трёх (ISO, SQL, ALZ).
  Также умеет парсить из `NYT::TNode` при спецификации формата (см. `TimeType`), в котором лежит время в ноде.
* `formatTime` — сериализует время в строку или в `NYT::TNode`, формат надо указать явно.
* `parseInterval` — парсит временной интервал в формате `%H:%M:%S`, при этом часы и минуты можно опустить. Есть версия, принимающая явный формат.
* `formatInterval` — сериализует временной интервал в формате `%H:%M:%S`, при этом часы и минуты не будут выведены, если они нулевые. Также есть версия с явно указанным форматом.

Также для `TimeType` есть реализация в питоне, для удобства работы с мапперами/редьюсерами.

### Пример

Также см. [тесты](tests/parse_time_test.cpp)

```cpp
#include <maps/analyzer/libs/parse_time/include/parse_time.h>

#include <library/cpp/yson/node/node.h>

namespace mp = maps::analyzer::parse_time;

void test() {
    auto tm = mp::parseTime("2021-02-03T10:20:30+04");
    std::cout << mp::toTimeT(tm.value()) << std::endl;
    std::cout << mp::yt::toDate(tm.value()) << std::endl;
    std::cout << mp::formatTime(tm.value(), formats::ALZ) << std::endl; // 20210203T062030Z
    std::cout << mp::formatTime(tm.value(), formats::DATE) << std::endl; // 2021-02-03

    auto dur = mp::parseInterval("1:23.123");
    std::cout << mp::formatInterval(dur.value()) << std::endl; // 01:23.123
    std::cout << mp::yt::toInterval(dur.value()) << std::endl;

    tm = mp::parseTime(NYT::TNode("2021-02-03T10:20:30+04"), mp::TimeType::String);
    std::cout << mp::formatTime(tm.value(), mp::TimeType::ALZ) << std::endl; // TNode("20210203T062030Z")
    std::cout << mp::formatTime(tm.value(), mp::TimeType::YtDate) << std::endl; // TNode(18661u)
    std::cout << mp::formatTime(tm.value(), mp::TimeType::YtDateTime) << std::endl; // TNode(1612333230u)

    tm = mp::parseTime(NYT::TNode(ui64(18661)), mp::TimeType::YtDate);
    std::cout << mp::formatTime(tm.value(), mp::TimeType::ALZ) << std::endl; // TNode("20210203T000000Z")
}
```
