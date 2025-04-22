# Webmail ipblocker worker

```
optional arguments:
  -h, --help            show this help message and exit
  --cbb-flag CBB_FLAG   cbb flag (default: 144)
  --cbb-net_flag CBB_NET_FLAG
                        cbb flag for blocking networks (default: 1044)
  --cbb-mtime-period CBB_MTIME_PERIOD
                        cbb mtime period (default: 5)
  --cbb-endpoint CBB_ENDPOINT
                        cbb endpoint (default: https://cbb-ext.yandex-team.ru)
  --sleep SLEEP         sleep period (default: 3)
  --ipset-id IPSET_ID   ipset id for ipv4 (default: ipblocker)
  --ip6set-id IP6SET_ID
                        ipset id for ipv6 (default: ip6blocker)
  --ipset-net-id IPSET_NET_ID
                        ipset id for ipv4 networks (default: ipblockernet)
    --ip6set-net-id IP6SET_NET_ID
                        ipset id for ipv6 networks (default: ip6blockernet)
  --ipset-timeout IPSET_TIMEOUT
                        ipset base timeout (default: 300)
  --yasm-port YASM_PORT
                        statserver port (default: 8082)
```

Тул запускается на инстансах кластера, добавляет в ipset списки для ipv4 и ipv6, блокирует их в iptables/ip6tables.

Ходит раз в `--sleep` секунд в ЕББ (флаг `--cbb-flag`), если там были изменения
за последние `--cbb-mtime-period` секунд, забирает списки IP и добавляет их в `ipset` с таймаутом `--ipset-timeout`. Если список большой, делает затухающий таймаут от `--ipset-timeout` до `--ipset-timeout`&times;2.

Отвечает на порту `--yasm-port` головановским сигналом с количеством записей в ipsetах.


## Собрать для mail_web_production

```bash
ya package -r --upload-resource-type=WEBMAIL_IPBLOCKER --owner=PS-FRONTEND --upload package.json
```

полученный id ресурса прописать в шаблонах для деплоя: \
https://a.yandex-team.ru/arcadia/yandex360/frontend/tools/docker-images/webmail-deploy/specs/front-app.j2?rev=r9515164#L5
