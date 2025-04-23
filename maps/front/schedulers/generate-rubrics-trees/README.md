# Генерация дерева рубрик

Генерирует деревья рубрик для каждого субрегиона заданного типа и выгружает их в MDS S3.

## General information

| Key | Value |
|---|---|
| Nirvana | https://nirvana.yandex-team.ru/flow/fbba3faf-d56e-4207-8985-1d2b29d73edc |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/rubrics/generate-rubrics-trees |
| Structure | https://bunker.yandex-team.ru/maps-front-showcase |
| **Result example** | `http://maps-front-showcase-int.s3.mds.yandex.net/rubrics/213-ru_RU.json` |

## Flow parameters

- `geo_id` - регион, в субрегионах которого будут сгенерированы деревья (например 225 - Россия).
- `locale` - язык.
- `min_company_count` - минимальное количество организаций в субрегионе, при котором будет сгенерировано дерево рубрик.
- `region_type_id` - ID типа субрегиона (например 6 - город, см. [libgeobase5](https://doc.yandex-team.ru/lib/libgeobase5/concepts/region-types.html)); должен соответствовать имени типа субрегиона
- `region_type_name` - имя типа субрегиона (например `city`, см. [YQL Docs - Geo](https://yql.yandex-team.ru/docs/yt/udf/list/geo/#georoundregion))

## Hot it works

1. Структура дерева рубрик и черный список рубрик выгружаются из [Бункера](https://bunker.yandex-team.ru/maps-front-showcase).
2. Выполняется YQL-запрос в [YT-таблицы Справочника](https://wiki.yandex-team.ru/sprav/altay/sprav-export-to-yt/sprav-yt-tables), формирующий список рубрик по каждому подходящему субрегиону и подсчитывающий количество организаций.
3. С помощью операции [Generate Rubric Trees](https://nirvana.yandex-team.ru/operations/1/filter?name=ExprStringEquals%28Generate%20Rubric%20Trees%29&deprecation=ExprFlowchartBlockTypeDeprecation%28active%29) формируется архив с файлами деревьев.
4. Архив выгружается в [MDS S3](http://maps-front-showcase-int.s3.mds.yandex.net/rubrics/213-ru_RU.json).
