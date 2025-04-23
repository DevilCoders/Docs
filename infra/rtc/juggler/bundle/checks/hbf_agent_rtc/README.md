# NAME

hbf_agent_rtc - yandex-hbf-agent daemon status check for RTC cluster.

# DESCRIPTION

Determine status of hbf-agent, if we can't get it - check if hbf-agent is running.
Check [wiki](https://wiki.yandex-team.ru/runtime-cloud/yandex-hbf-agent/) for details.

# SEVERITY

Critical.

# DIAGNOSTICS

    curl -v 'localhost:9876/status'
    portoctl list | grep hbf-agent

# FAST FIX

Read diagnostic message, try restart hbf-agent, check if it is enabled.

# KNOWN ISSUES

None.

# RESPONSIBLE

[Network infra](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_mondev_6921/)

# RELATED TICKETS

None.
