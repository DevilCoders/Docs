# Генератор сайтмапов для веб-карт

Service for generating [sitemaps](https://www.sitemaps.org/ru/protocol.html) for yandex.{tld}/maps

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-maps-sitemap/ |
| Reactor | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/seo/generate-sitemaps |
| Nirvana | https://nirvana.yandex-team.ru/flow/10ca8b3d-8b65-4453-9eaf-e6a44daaaa74 |

## Storage

MDS S3 bucket: [s3-maps-front-sitemaps](https://abc.yandex-team.ru/services/maps-front-maps-sitemap/resources/?show-resource=5931442)

## Vault

| Type | URL |
|---|---|
| Testing | https://nirvana.yandex-team.ru/secret/ba82f857-c9d9-4ce3-96f4-e61b0d621c60 |
| Production | https://nirvana.yandex-team.ru/secret/7ee57ac1-1c5d-4ac0-b6b8-b66be7fa9986 |

## Data Sources

Таблица с [организациями](https://yql.yandex-team.ru/Operations/Xnm-pGHljkJFTEs_WRbQoIauT1EKwJozn8UNheJy_3c=). Обновляется [шедулером](https://jam.stat.yandex-team.ru/statobj/yql/d3aa124f-227b-4b1d-ab3f-241a880f4565/). В основе данные справочника и две таблички геопоиска.

Таблица с рубриками: экспорт из Алтая, данные обновляет Справочник.

Для генерации данных по топонимам используется https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/houses_generator/. Обновляется [шедулером](https://sandbox.yandex-team.ru/scheduler/19189/view).

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/check_details/?host=maps-front-schedulers&service=%2Fmaps%2Ffront%2Fmaps%2Fseo%2Fgenerate-sitemaps_failure |
| Solomon | https://solomon.yandex-team.ru/admin/projects/maps-front-schedulers/alerts/_maps_front_maps_seo_generate-sitemaps_failure |

## Dashboards

| Name | URL |
|---|---|
| s3-maps-front-sitemaps | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=s3-maps-front-sitemaps |

## Documentation

[DOC](DOC.md)

## Known clients

[Веб-Карты](https://abc.yandex-team.ru/services/maps-front-maps/)

## What happens when service is down

Поисковые роботы могут пропустить страницы, а так же качество и скорость индексации могут стать ниже. Тем самым трафик с поисковых систем, например таких как Google может значительно понизиться.

## How to fix common problems

N/A

## Developing

[CONTRIBUTING](CONTRIBUTING.md)
