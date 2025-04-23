# NAME

tcp_sampler_dump checks that sampler runs and saves dump 2 times a day.

# DESCRIPTION

Check last modify timestamp of dump.

# SEVERITY

Warning.

# DIAGNOSTICS
    which tcp-sampler
    ls -lt /tmp/tcp-sampler.message.dump

# FAST FIX

Try run `sudo tcp-sampler`, if it fails try `sudo tcp-sampler -debug -nopush 2>out`.

# KNOWN ISSUES

None.

# RESPONSIBLE

[Network infra](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_mondev_6921/)

# RELATED TICKETS

https://st.yandex-team.ru/RTCNETWORK-361
