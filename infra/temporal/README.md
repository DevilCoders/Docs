![](./temporal.png)

* `./swat` — things specific to `swat-temporal.yandex.net` [installation](https://wiki.yandex-team.ru/awacs/temporal/ops/installation/).
* `./activities` — [activities](https://docs.temporal.io/docs/concepts/activities) code.
   They are meant to be reusable between different workflows.
* `./workflows` — [workflows](https://docs.temporal.io/docs/concepts/workflows) code.
   Some of them are meant to be reusable.
* `./clients` — clients for communicating with different Yandex services.
   Some of them are very ad-hoc and not fully fledged, and thus kept not in `/contrib`, but there.
* `./cmd` — [workers](https://docs.temporal.io/docs/concepts/workers) that run workflows and activities.

See our [wiki docs](https://wiki.yandex-team.ru/awacs/temporal/) for more details.
