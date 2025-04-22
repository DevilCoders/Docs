## Description
"Best rating" (or "Top-rated") filter is used to leave only the best companies in search results (restaurants, cafes, hotels, etc. having high rating in Sprav).

Rating filtering threshold depends on a rubric and a region. The default is 4.0. For example, a cafe in Moscow is considered "the best" if its rating is at least 4.2.

## Data Source
 * `city_rank.jsonl` is obtained from `//home/sprav/assay/common/CityRank` table (YT Hahn).
 * `ratings.jsonl` is built using YQL query: https://yql.yandex-team.ru/Operations/XBDbXTa9vEGk2C_hpi1qz55Ee13FG91angk2YHc2UTw=

## Tickets
See GEOSEARCH-5216 and ALTAY-9222 for reference.
