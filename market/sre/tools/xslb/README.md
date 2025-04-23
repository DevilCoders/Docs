# yandex-market-xslb

Utilities to work on xSLB-servers:
* `/usr/lib/yandex/market/xslb/updatevips` – this utility is called with cron every 3 minutes. It checks racktables for VIP-address (addresses of VS) for current host and if it finds, that something is missing on current host, it adds'em and calls `configure_interfaces` to update `/etc/network/interfaces`

### Links

[sandbox job to build debian package](https://sandbox.yandex-team.ru/task/141679145/view)
