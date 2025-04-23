## yandex-market-ipip4-tunnel

Скрипт для поднятия ipip4 НОК туннеля

### links
[Sandbox task](https://sandbox.yandex-team.ru/task/237284044/view)
[Организация IPv4 доступа для IPV6-only серверов](https://wiki.yandex-team.ru/NOC/IPv6to4/)
[NOC ipv4 mapping](https://racktables.yandex-team.ru/index.php?page=ipv4net&tab=map64&id=8026&hl_ip=5.255.198.13)

### How-to
1. прописать в [NOC ipv4 mapping](https://racktables.yandex-team.ru/index.php?page=ipv4net&tab=map64&id=8026&hl_ip=5.255.198.13) маппинг
2. дождаться пока прорастёт в выгрузку https://racktables.yandex.net/export/map64.txt
3. запустить скрипт /etc/network/if-up.d/zz-noc-ipip или перегрузить хост

**Disclaimer:**
1. не прописывать ptr в днс иначе self-dns пропишет их в А зоне
2. не забываем снимать nat64 тег в кондукторе
