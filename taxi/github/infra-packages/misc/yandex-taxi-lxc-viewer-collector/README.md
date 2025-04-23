# yandex-taxi-lxc-viewer
Скрипт сбора информации о LXC-контейнерах

- cron:
 -- 00 * * * * root /bin/bash /usr/lib/yandex/taxi-lxc-viewer-collector/lxc-viewer-collector.sh
- endpoint:
 -- http://lxc-viewer.taxi.yandex.net/add_host
