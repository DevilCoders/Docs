Небольшая утиля для генерации "правильных" ipv6 адресов для mtn и static vlan сетей. Поддерживает генерацию EUI-64 и host-id вариантов адресов.

Пример использования:
```shell script
ipaddrgen --help
Usage of ipaddrgen:
  -h, --hostname string   hostname for host-id address format
  -m, --mac string        mac for eui-64 address format
  -n, --network string    network with prefix
  -p, --projectID int     projectid for mtn networks
  -t, --type string       address type(eui64|host-id) (default "eui64")

ipaddrgen -n 2a02:6b8:0:5409::/64 -m 52:54:00:9e:8f:d2  -h whslb-01tom.market.yandex.net -t eui64
2a02:6b8:0:5409:5054:ff:fe9e:8fd2

ipaddrgen -n 2a02:6b8:0:5409::/64 -m 52:54:00:9e:8f:d2  -h whslb-01tom.market.yandex.net -t host-id
2a02:6b8:0:5409::6de8:7321
```
Так же возможно использование как библиотеки

```go
package main

import (
	"a.yandex-team.ru/market/sre/tools/ipaddrgen/pkg/ipaddrgen"
	"fmt"
)
func main() {
    params, _ := ipaddrgen.NewNetworkParams("2a02:6b8:0:5409::/64", "52:54:00:9e:8f:d2", "whslb-01tom.market.yandex.net", 577)

	addr, _ := params.GetEUI64Addr()
    fmt.Println(addr.String())

    addr, _ = params.GetHostIdAddr()
    fmt.Println(addr.String())
}
```
