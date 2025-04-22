# NAME

hostman\_server - check hostman server serve http requests.

# DESCRIPTION

Active check, perform GET `/unistat` requets to hostman servers on 8080 port

# SEVERITY

Critical.

# DIAGNOSTICS

    whet -O - "{hostname}:8080/unistat"

where hostname from
[hostman servers list](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/search_runtime/minion/runtime.jinja)

# FAST FIX

FIXME.

# KNOWN ISSUES

None.

# RESPONSIBLE

[SRE RTC](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_cross/)

# RELATED TICKETS

None.

# SEE ALSO

Hostman server
[docs](https://a.yandex-team.ru/arc/trunk/arcadia/infra/ya_salt/server)
