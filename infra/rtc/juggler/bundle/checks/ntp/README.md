# NAME

`ntp` - check ntpd status

# DESCRIPTION

This check collects output of multiply subcommands of ntpq and ntpdc.

Overall system ntpd status gets by `rv` and additional - by 'sysstat' subcommand. Unworking Ntpd as process detected by empty output in stdout  - ntpq/ntpdc don't set error code in this case.
Overall system status returned in status field
`status=0628 leap_none, sync_ntp, 2 events, no_sys_peer,`
First 4 hexadecimal values encodes state, tailed by its text representations, separated by comma.  Last representation (`no_sys_peer` in example) is a last event. Not all status changes reflects by event, so this value can make  confuse. Overall functionality checks by 2nd field - source. if it set to `0=sync_unspec` - all is awfully and not working at all. Some timeout made for warm-up. It seems to be 1 minute enough. If we have status `ntp_sync` its not mean what we have synced clock, but what we have protocol working.
If startum is too high - alert is fired. In our case we checks stratum not more 4 - our Ntp servers have stratum 2, so clients will be stratum 3. If 5 or more - something wrong.
Ntpd makes calibration of hardware clocks in hour or close, so if uptime is less than hour - WARN fired.
Check collects list of peer by `as` subcommand. From available quality servers algorithm selects  one `sys.peer` (primary source) and two `candidate`. For normal sync is needed all three servers. Other servers will be `outlier` or `backup`. Peers with statuses `reject` or `falsetick` shows what we have broken Ntp servers.

# ERROR DESCRIPTION AND SEVERITY

- `OK:   status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - normal status with info.
- `WARN: status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - status in warm-up time. No other check will be made
- `CRIT: no sync, status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - Ntp protocol not work, we don't know sampling server and cannot calculate our problems.
- `WARN: ntpd started less then 1 hour ago, status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - Uptime <1 hour.
- `CRIT: stratum too high, status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - Ntpd startum is 5 or above. 16 set with out of sync, then protocol not functional.
- `CRIT: no primary ntp sync server, status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - Primary sync server (`sys.peer`) not found.
- `WARN: too few candidates for sync, status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - Secondary sync servers (`candidate`) less than two
- `WARN: invalid peers detected, status: xxxxxxxx; stratum: xxx; offset: xxxx; uptime: xxxx.`
  - Found Ntp servers with broken protocol

[PCI-DSS](../PCI-DSS.md) related. Crits should be immediately reported to
[Hostman duty engineer](https://abc.yandex-team.ru/services/hostmanager/duty/)

# DIAGNOSTICS

    service ntp status
    ntpq -nc rv
    ntpq -nc as
    ntpq -nc sysinfo / ntpdc -nc sysinfo
    ntpq -nc sysstat / ntpdc -nc sysstat
    ntpq -nc rv <assid>` - where <assid> get from `ntpq -nc as` output

# FAST FIX

Restart?

# KNOWN ISSUES

None

# RESPONSIBLE

[Hostman team](https://abc.yandex-team.ru/services/hostmanager/)

# RELATED TICKETS

[HOSTMAN-755](https://st.yandex-team.ru/HOSTMAN-755)  
