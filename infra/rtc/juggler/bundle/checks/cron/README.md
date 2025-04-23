# NAME

cron - cron daemon status check

# DESCRIPTION

Check pidfile contain pid, it's process is running or sleeping and it's binary
is cron.

# SEVERITY

Critical.

# DIAGNOSTICS

    pgrep cron
    ps uwwp `cat /var/run/crond.pid`

# FAST FIX

Restart process.

# KNOWN ISSUES

None.

# RESPONSIBLE

[SRE RTC](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_cross/)

# RELATED TICKETS

None.
