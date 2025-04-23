# Juggler agent config files for RTC

## How to build package manually

    ya package --debian --checkout --not-sign-debian pkg.json

## How to release new package

Deb package will be automatically built and deployed to search deb repo by
[testenv](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/runtime_cloud/BuildRuntimeCloudPackages.yaml)
when changes committed to svn.

## How to deploy new package

TODO(mixas): docs will be added when completed migration from
[old package.](https://bb.yandex-team.ru/projects/JUGGLER/repos/config-juggler-search/browse)

## See also

https://wiki.yandex-team.ru/sm/juggler/

## Feedback

Feel free to [make a ticket](https://st.yandex-team.ru/createTicket?type=1&assignee=mixas&priority=2&queue=HOSTMAN)
if you spotted a bug or have a feature request.
