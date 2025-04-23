# Node info
yandex-rtc-nodeinfo (former part of ya-salt) collects info about host environment and pushes it to YP clusters.

Deployment is controlled by unit `yandex-rtc-nodeinfo` of `core` repo.

Typical deployment action:
* commit code
* wait build
* update `yandex-rtc-nodeinfo.yaml` with desired version change
* push changed unit to core repo


    hmctl push yandex-rtc-nodeinfo.yaml -r core -m 'TICKET-NUM: <commit description>' -c <cluster list>


* commit updated unit to arcadia
