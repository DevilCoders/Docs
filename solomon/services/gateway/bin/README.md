## Build

```bash
$ ya make
```

## Run

```bash
$ ./run.sh --enable-preview -Dru.yandex.solomon.LabelValidator=skip -Djava.net.preferIPv6Addresses=true \
    ru.yandex.solomon.gateway.GatewayMain \
    --config /path/to/gateway.conf \
    --secrets /path/to/decrypted/gateway.secrets
```
The path `/path/to/decrypted/gateway.secrets` must point to decrypted secrets, opposed to encrypted secrets that can be found
in solomon/config/... directories. To decrypt them locally use
```bash
$ cd arcadia/solomon/tools/secrets
$ ya make
$ ./secrets decrypt --in ~/arcadia/solomon/configs/.../gateway.secrets --out /path/to/decrypted/gateway.secrets
```
