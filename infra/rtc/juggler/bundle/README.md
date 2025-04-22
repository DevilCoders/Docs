# Juggler checks deb-bundle for RTC

# Key points

* Python
  * Native for SRE
  * Inheritance
  * Convenient testing
* Arcadia and static builds
  * Much more chances to survive on corrupted filesystems
  * Independence from system python/libs (no depends issues on hosts)
  * Single binary saves resources
  * Code reuse (contrib, local libs)
* Deb package
  * Industrial standard
  * Dependencies, versions and changelogs
  * Debug friendly (logging, debsums etc.)
* Deploy
  * Stages!
  * Standard deploy workflow (Salt)
  * Debug friendly (any host, any version, salt debug tools, dashboards etc.)

A bit more info with comparsion to previous bundle available in
[RUNTIMECLOUD-8889](https://st.yandex-team.ru/RUNTIMECLOUD-8889)

# Conventions

* Each check should have own package inside `checks/` directory. Check may have
  subchecks, in this case subchecks should be located in same package.
* Each check should have `tests` subdirectory and at least one test in it
* Each check should have `README.md` it it's directory, see `cron/README.md` as
  format example.
* Check's name must reflect what is being monitored without any boilerplate
  words. This means when one need to monitor cron daemon, check should be
  simply named `cron`, neither `cron_check` nor `check_cron`.
* Check's name should be all lower case with underscore for words delimiter.
* Exceptions should be handled and turned to easy readable juggler crits/warns
  (backtraces in juggjer are almost useless and just pollute aggregator's
  descriptions).

# Non-pythonic checks

See [external](./external/) subdirectory.

# HOWTO

## How to add new check to the bundle

See [contributing](#contributing) if you unfamiliar with ya build tool.

0. Read [conventions](#conventions) first.
1. Copy `checks/cron` dir to `checks/{new_check_name}`
2. Replace code, tests and docs with your own
2. Register it in `checks/__init__.py` and `checks/ya.make`
4. Run tests (`ya make -t`)
5. Commit changes.

## How to build bundle manually

    ya package --debian --checkout --not-sign-debian deb/package.json

## How to release new bundle

Deb package will be automatically built and deployed to `search` deb repo  by
[testenv](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/runtime_cloud/BuildRuntimeCloudPackages.yaml)
when changes committed to svn. List of created packages available in
[sandbox](https://sandbox.yandex-team.ru/resources?author=mixas&type=YA_PACKAGE&limit=20&attrs=%7B%22resource_name%22%3A%22yandex-rtc-juggler-bundle%22%7D)

## How to deploy new bundle

1. Check package availability using command (package with your commit number
in version should be listed in output).

    `apt-cache policy yandex-rtc-juggler-bundle`

2. Set version in [spec file](https://bb.yandex-team.ru/projects/RTCSALT/repos/core/browse/units.d/yandex-rtc-juggler-bundle.yaml).
3. Make a PR to apropriate branch (`prestable`, `sas`, `vla`, `man`, `msk`).

That's it, juggler bundle follows standard `hostctl` deploy pipeline.

## How to debug on hosts

Checks may be runned using juggler client:

    jclient-api print-events
    jclient-api run-check --service cron

or directly:

    /var/lib/rtc/juggler.d/rtc-juggler-bundle/pythonic/bundle --execute-check cron

## How to rename existing check

To seamlessly and safely change check name, follow steps from
[How to add new check to the bundle](#How-to-add-new-check-to-the-bundle), but
use `svn cp` to preserve commit history.

When bundle with new check is deployed, it's time to make aggregates for it,
see [How to add new aggregate](../reconf/HOWTO.md#How-to-add-new-aggregate)

When aggregates for new check deployed, old aggregates may be removed from
Juggler. And only then, old check should be removed from bundle.

JFI: There is another way to rename check (which may looks faster at first
glance: emitting two events from same check), but this approach is more
error-prone (check must be moved to `run_always` mode to avoid
aggregate/bundle names mismatch) and should be avoided when possible.

# Contributing

## Build tool reference

[ya](https://wiki.yandex-team.ru/yatool/)
[ya dist](https://wiki.yandex-team.ru/yatool/distrib/)
[ya test](https://wiki.yandex-team.ru/yatool/test/#testynapytest)

## Get sources

    ya clone --no-junk ./arcadia && cd ./arcadia
    ya make -j0 --checkout infra/rtc/juggler/bundle
    cd infra/rtc/juggler/bundle

## Build sources

    ya make

## Run tests

    ya make -t

# Feedback

Feel free to [make a ticket](https://st.yandex-team.ru/createTicket?type=1&assignee=mixas&priority=2&tags=juggler-bundle&queue=RUNTIMECLOUD)
if you spotted a bug or have a feature request.
