# NAME

rsyslog - configure rsyslog and keep it up and running

# DESCRIPTION

Install deb package with system logs rotation rules and manage daemon.

# DIAGNOSTICS

    hostctl status rsyslog
    systemctl status rsyslog.service

# MONITORING

[PCI-DSS](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/checks/PCI-DSS.md)
related. Crits should be immediately reported to
[Hostman duty engineer](https://abc.yandex-team.ru/services/hostmanager/duty/)

# KNOWN ISSUES

None.

# RESPONSIBLE

[Hostman team](https://abc.yandex-team.ru/services/hostmanager/)

# RELATED TICKETS

[HOSTMAN-597](https://st.yandex-team.ru/HOSTMAN-597)
