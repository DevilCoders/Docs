# sync-deleted-uids

## General information
| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-constructor-int/ |
| Nirvana | https://nirvana.yandex-team.ru/flow/9e21896c-bb79-474f-938d-852d9e496876/ |
| Reaction | https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/constructor-int |

Daily scheduler to delete constructor maps of [deleted users](../../CONTRIBUTING.md#processing-deleted-accounts).

- Written in Python 3.
- Built with [ya make](https://docs.yandex-team.ru/ya-make/), which produces a standalone executable file.
- The executable is then uploaded to [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/schedulers/binary/constructor-int) using [bean](https://a.yandex-team.ru/arc_vcs/maps/front/packages/bean).
- Reaction is managed by [lama](https://a.yandex-team.ru/arc_vcs/maps/analytics/tools/lama) with [binary scheduler](https://a.yandex-team.ru/arc_vcs/maps/analytics/tools/lama/presets/projects/maps-front/binary-scheduler.jinja) preset.

## Building

To build for debug run:

```sh
make build
```

To build for release run:

```sh
make build-release
```

If the build fails on MacOS with `failed with exit code -9` error, then try building with `YA_USE_CLONEFILE=1` env variable:

```sh
YA_USE_CLONEFILE=1 make build

# same for release build
YA_USE_CLONEFILE=1 make build-release
```

This is a [known issue](https://clubs.at.yandex-team.ru/arcadia/24117) that happens only on some MacOS sytems.

## Testing

There are integration tests for this scheduler, but at the moment they can only be run locally and not in CI, because they require an OAuth token for YT and YQL.

See [Processing deleted accounts](../../CONTRIBUTING.md#processing-deleted-accounts) for the instructions on how to run these tests.

## Releasing

Run `npm version patch` to bump version in `package.json`, `lama/testing/lama.yaml` and `lama/production/lama.yaml`. This command will also upload the binary for testing and production to [hahn.[home/maps/front/schedulers/binary/constructor-int]](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/schedulers/binary/constructor-int) in YT.

Commit the changed files and submit a PR. Once the PR is merged into trunk, [the reactions](https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/constructor-int) will be updated during the next "lama sync".

## What happens if the scheduler is down

If the scheduler is down, maps of users deleted from passport will not be automatically deleted from constructor, which may pose problems under GDPR law in EU.

## Troubleshooting

Inspect the `stderr.log` logs of the "Maps.Front Binary Scheduler" block of the binary scheduler graph in Nirvana.

### RuntimeError: Got too many uids to delete

There is a limit on the number of users that can be deleted during a single run of the scheduler. If this limit is exceeded, the scheduler will fail with `RuntimeError: Got too many uids to delete: count > limit`. Where `count` is the number of users to be deleted and `limit` is the current limit.

Looking at the statistics of the previous runs, it was decided to set the default value of the limit to 100 users per day. Since, it is rare that more than 100 users get deleted from the passport database in a single day.

If you've encountered this error, please look at the value of the `count` number to decide which action to take next.

#### Set the downtime and delegate the issue to maintainers

If the `count` is much greater than the current limit, set the downtime of the monitoring alert until the next work day and summon someone from the [maintainers team](https://abc.yandex-team.ru/services/maps-front-constructor-int/).

#### Rerun the scheduler once with an overriden limit

If the `count` is slightly greater than the current limit (e.g. if `count <= 1000`), you can just rerun the scheduler once with an increased limit:

1. Open the [manual trigger](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Ffront%2Fconstructor-int%2Fsync-deleted-uids_production_manual-trigger) artifact in Reactor.
2. Click on "Instantiate" button.
3. In the opened window, enter the `count` number into the "Value" input field and click on "Instantiate".

The new instance of the artifact should trigger a launch of the [reaction](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Ffront%2Fconstructor-int%2Fsync-deleted-uids_production) with the limit overriden by the number from the artifact. This override will be effective only for this launch, and the default value of the limit will be used next time, when the reaction is triggered by the cron.
