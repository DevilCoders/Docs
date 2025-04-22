# NAME

bind - Check local DNS resolver

# DESCRIPTION

Check working of local DNS resolvers and cachers. Test scenario passed as arguments of aggregation
Each argument separated by `'#'` symbol in 2 or 3 fields:

``` name # dns [#flags]```

`Name` field consists of one o more names, separated by comma (`,`). All names are checked with same DNS servers and options, if any name fails check alert is raised.
`DNS`  field consists of one o more servers, separated by comma (`,`). Resolver made requests to all servers in same time.
`Name` or `DNS` item may be `@bb_ip` or `@fb_ip` which is substituted by host's BackBone or FastBone address. Addresses for substitution are collected from `ya-netconfig state` output
Optional field `flag` now can have only one flag - `A_unwanted`.
If this flag set then alert fires up if `A` answer received

If no arguments set default check
- `DNS: '127.0.0.1', '::1', '@bb_ip'`
- `Names: 'ya.ru', 'github.com'`

will be produced.

RTC local cache, accessible by `fd64::1` must return `AAAA` record, even if domain name have only `A` record in outside DNS
Domain names for this check must return A records or both. Better - `A` record only - for example, `github.com`

# ERROR DESCRIPTION

- `CRIT ns=[...] <Exception description>` CRIT returned on any exception raised by dns.resolver, such as NXDOMAIN, Server or socket error. NoAnwer = empty record by selected type is NOT error and suppressed in code. So if that error raised - something happen with library.
- `CRIT Empty answer returned` Both A and AAAA requests returns empty records
- `CRIT DNS Type A record returned but unwanted` A request returns record, but it's incorrect, flag `A_unwanted` was set for this test

# SEVERITY

Critical.

# DIAGNOSTICS

In Search Runtime all DNSes are served by one BIND instance. So check BIND, and then upper DNSes. In Qloud or other environments unbound was used. Usually service named `unbound64` for `fd64::1` cacher and unbound53 for `fd53::1`

# FAST FIX


# KNOWN ISSUES

None.

# RESPONSIBLE

[SRE RTC](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_cross/)
