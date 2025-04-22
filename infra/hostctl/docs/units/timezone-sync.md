# NAME

timezone-sync - keep actual timezone

# DESCRIPTION

Set `Europe/Moscow` from time to time using systemd timer.

# DIAGNOSTICS

    hostctl status timezone-sync
    cat /etc/timezone

# MONITORING

[PCI-DSS](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/bundle/checks/PCI-DSS.md)
related. Crits should be immediately reported to
[Hostman duty engineer](https://abc.yandex-team.ru/services/hostmanager/duty/)

# KNOWN ISSUES

None.

# RESPONSIBLE

[Hostman team](https://abc.yandex-team.ru/services/hostmanager/)

# RELATED TICKETS

[HOSTMAN-696](https://st.yandex-team.ru/HOSTMAN-696)
