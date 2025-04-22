# Duty engeneers permissions on RTC clusters

This package provide capability to run `tcpdump` without root privileges and
brings several sudo rules for duty engeneers (NOC and support teams).  
See details in [HOSTMAN-595](https://st.yandex-team.ru/HOSTMAN-595) and
[HOSTMAN-615](https://st.yandex-team.ru/HOSTMAN-615)

## How to build package manually

    ya package --debian --checkout --not-sign-debian pkg.json
