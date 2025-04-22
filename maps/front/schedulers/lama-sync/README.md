# lama-sync

Made with (@yandex-int/bean)[https://a.yandex-team.ru/arc_vcs/maps/front/packages/bean].

## General information
| Key | Value |
|---|---|
| Nirvana | https://nirvana.yandex-team.ru/flow/468dfc7f-08f9-43a9-8ea0-f4b4b90103b9 |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/arcadia/lama-sync |

Scheduler to sync `lama.yaml` configs in https://a.yandex-team.ru/arc_vcs/maps/front excluding `quarantine` directory

## How it works

Scheduler fetches lama.yaml config paths by file regexp using [FCS](https://abc.yandex-team.ru/services/arcadiacodesearch). Then the configs are downloaded using Arcanum API and synced by [lama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama) CLI

## What happens if scheduler is down

Updates to lama.yaml configs merged in trunk will not be applied automatically. Schedulers' maintainers can update their own reactions manually.
