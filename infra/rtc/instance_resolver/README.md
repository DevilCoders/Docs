# Motivation

Resolve services and their owners on physical hosts or switches.

# Implementation

Service didn't store anything (expect some in-memory caches), it's a simple proxy.
It uses https://staff.yandex-team.ru/robot-rtc-iresolver for authorization.

# Resolving logic

For Nanny resolver will use all users and groups from service.

For ABC service resolver try to filter all persons without administration role, if it's possible.

# UI

Go to https://instance-resolver.in.yandex-team.ru.

# notifyctl

You can use [notifyctl](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/notifyctl) to send emails to service responsibles.

# API

Check https://instance-resolver-api.in.yandex-team.ru for documentation.

To obtain tvm service ticket use:

    ya tool kvmknife get_service_ticket sshkey --src 2013412 --dst 2013412

Put ticket into `X-Ya-Service-Ticket` header. Service located in network macro `_RTC_INSTANCE_RESOLVER_NETS_`,
use it to get access through puncher.

You should have `tvm ssh user` role in abc service [RTC Instance Resolver](https://abc.yandex-team.ru/services/rtc_instance_resolver/) to use `ya tool kvmknife`.

# Monitoring

* [Juggler](https://juggler.yandex-team.ru/dashboards/rtc-instance-resolver/)
* [Golovan](https://yasm.yandex-team.ru/template/panel/rtc_instance_resolver/)

# Examples

Resolve instances on given host:

    curl https://instance-resolver-api.in.yandex-team.ru/v1/host_instances/sas1-1234.search.yandex.net

Resolve instances located in specified switch with custom timeout:

    curl -H "Grpc-Timeout: 60000m" https://instance-resolver-api.in.yandex-team.ru/v1/switch_instances/sas1-s1

# Deploy

* [TestEnv](https://beta-testenv.yandex-team.ru/project/runtime_cloud/job/YANDEX_RTC_INSTANCE_RESOLVER_DAEMON/history?limit=20)
* [Nanny](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc-instance-resolver-production/)
* [UI](https://nanny.yandex-team.ru/ui/#/services/catalog/instance-resolver-ui/)
* [Wiki](https://wiki.yandex-team.ru/runtime-cloud/instance-resolver/)
* [Awacs](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/instance-resolver/show/)
* [Docs](https://docs.yandex-team.ru/rtc/instance-resolver)
* [Metrika](https://metrika.yandex.ru/dashboard?group=day&period=week&id=74506744)
