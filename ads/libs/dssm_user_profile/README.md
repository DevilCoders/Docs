Что делает
----------
Принимает профиль пользователя и вынимает из него необходимые факторы по списку аннотаций
```cpp
  TVector<TString> Extract(const TBigbPublicProto& profile, const TParams& params)
```
Возвращает список строк, которые подаются на вход dssm.

Детали
------
[TFieldsExtractor](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/dssm_user_profile/extractor.h?blame=true&rev=6679106#L25) 

  парсер, не поддерживает многопоточность, т.к. имеет внутренний стейт.

[TFieldsExtractorPool](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/dssm_user_profile/extractor.h?blame=true&rev=6679106#L69) 

  парсер с поддержкой многопоточности за счет пула дефолтный парсеров.

Какие факторы реализованы (аннотации)
-------------------------------------
[enum_fields.h](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/dssm_user_profile/enum_fields.h)

Пример
------
```cpp
TFieldsExtractor extractor({"queries", "visit_goals"});
auto res = extractor.Extract(profile, {now, now, geoLookup, nullptr, nullptr, true, false})
EXPECT_THAT(res, ElementsAreArray(
    {
        R"({"queries_logtimesago": [], "queries_sources": [], "queries_daysago": [], "queries": []})",
        "0 1 2"
    }));
```
