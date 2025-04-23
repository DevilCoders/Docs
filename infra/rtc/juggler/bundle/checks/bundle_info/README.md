# NAME

bundle\_info - checks bundle version control check

# DESCRIPTION

Smallest possible check, all it's does is show bundle name and version.
Unable to emit any status except OK. `NO DATA` means juggler agent is dead or
have no resources to run checks.

# SEVERITY

Critical.

# DIAGNOSTICS

    dpkg -l | grep yandex-rtc-juggler-bundle
    /var/lib/rtc/juggler.d/rtc-juggler-bundle/pythonic/bundle --version
    /var/lib/rtc/juggler.d/rtc-juggler-bundle/pythonic/bundle --execute-check bundle_info

# FAST FIX

    sudo apt-get install yandex-rtc-juggler-bundle

# KNOWN ISSUES

None.

# RESPONSIBLE

[SRE RTC](https://staff.yandex-team.ru/departments/yandex_mnt_sa_runtime_cross/)

# RELATED TICKETS

None.
