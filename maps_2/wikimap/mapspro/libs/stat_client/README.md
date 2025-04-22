Stat Client Library
===================
Provides an easy way to prepare and upload reports to [Yandex Stat](https://stat.yandex-team.ru).


Upload
------
The upload mechanism is able to send reports prepared by means of this library:
```cpp
#include <maps/wikimap/mapspro/libs/stat_client/include/upload.h>

void upload(
    const std::string& statUploadApiUrl,
    const ShinyDailyReport& report)
{
    try {
        stat_client::Uploader(statUploadApiUrl).upload(report);
    } catch (const stat_client::ReportUploadError &e) {
        ERROR() << e.what();
    }
}
```

As well as reports in form of plain text, potentially prepared outside of this library:
```cpp
#include <maps/wikimap/mapspro/libs/stat_client/include/upload.h>

void uploadShinyDailyReport(
    const std::string& statUploadApiUrl,
    const std::string& csvTable)
{
    try {
        stat_client::Uploader(statUploadApiUrl).upload(
            "Maps.Wiki/ShinyReports/ShinyReport",
            csvTable,
            Scale::Daily
        );
    } catch (const stat_client::ReportUploadError &e) {
        ERROR() << e.what();
    }
}
```

**Good to know**. To obtain Yandex Stat upload API URL from `services.xml` a convenience function can be used:
```cpp
#include <yandex/maps/wiki/common/extended_xml_doc.h>
#include <yandex/maps/wiki/common/stat_utils.h>

const common::ExtendedXmlDoc config("/etc/yandex/maps/wiki/services/services.xml");
const auto statUploadApiUrl = common::getStatUploadApiUrl(config);
```


Reports Preparation
-------------------
In prinicple, a report is a mapping of dimensions to measures. There is a convenience template class `Report` that provides this kind of mapping and able to dump data in CSV format. This dump could be upload to Yandex Stat or, for example, saved on disk for examination.


### Example
```cpp
#include <maps/wikimap/mapspro/libs/stat_client/include/report.h>

using introspection::operator==;

class Dimensions {
public:
    Dimensions(chrono::TimePoint fielddate, const std::string& region)
        : fielddate_(std::chrono::round<chrono::Days>(fielddate))
        , region_(region)
    {}

    auto introspect() const { return std::tie(fielddate_, region_); }

    static void printHeader(csv::OutputStream& os) { os << "fielddate" << "region"; }

    void print(csv::OutputStream& os) const {
        os << chrono::formatIntegralDateTime(fielddate_, "%Y-%m-%d") << region_;
    }

private:
    std::chrono::time_point<std::chrono::system_clock, chrono::Days> fielddate_;
    std::string region_;
};

struct Measures {
    size_t activeUsers;
    size_t moderatedTasks;

    static void printHeader(csv::OutputStream& os) { os << "active_users" << "moderated_tasks"; }
    void print(csv::OutputStream& os) const { os << activeUsers << moderatedTasks; }
};

struct ShinyDailyReport: public stat_client::Report<Dimensions, Measures, stat_client::Scale::Daily> {
    ShinyDailyReport(): Report("Maps.Wiki/ShinyReports/ShinyReport") {}
};

```

**Note**. `Dimensions` class must be introspectable, whereas `Measures` must be default contructible and comparable by `==`.

**Warning**. It is a good idea to have duration of `fieldate_` of the same size as scale. Otherwise, two different timepoints can result in the same output when they are print. Thus an invalid Yandex Stat input with the same dimension appeared twice can be generated.

This report can be populated with data in the following manner:
```cpp
const auto now = chrono::TimePoint::clock::now();

ShinyDailyReport report;
report[Dimensions(now, "cis")] = {100500, 42};
```
