## Локальный запуск morda-go

Суть: запускается reverse proxy на дев-стенде, готовый к проксированию соединений с дев-стенда на локальную машину.

 {% note alert %}
 
 Способ не самый секурный, вместо reverse proxy лучше использовать ssh туннель. Но FRP быстрее и автоматически.
 
 {% endnote %}

### сервер

```
$ wget https://github.com/fatedier/frp/releases/download/v0.39.0/frp_0.39.0_linux_amd64.tar.gz
$ tar xfv frp_0.39.0_linux_amd64.tar.gz
$ sudo mv frp_0.39.0_linux_amd64 /opt/frp
$ cd /opt/frp/
$ sudo chown `whoami`. -R .
$ vim frps.ini
```

Контент конфига:
```
[common]
token=not_var{{server token}} # например 'openssl rand -hex 48'
bind_port = 22050
allow_ports = 10000-24100
```

Далее сервер запустить, самый простой вариант это screen:
```
$ screen -R
$ ./frps -c ./frps.ini
```


### Клиент

```
$ brew install frpc
$ vim /opt/homebrew/etc/frp/frpc.ini
```

Контент конфига:
```
[common]
server_addr = v133.wdevx.yandex.net
server_port = 22050
token=not_var{{server_token}}
tls_enable = true

[mordago]
type = tcp
local_ip = 127.0.0.1
local_port = 20400
remote_port = 20400
use_encryption = true
use_compression = true
```

Далее запустить как сервис - `brew services restart frpc`.
Или запустить "интерактивно" - `/opt/homebrew/opt/frpc/bin/frpc -c /opt/homebrew/etc/frp/frpc.ini`.

Чтобы бинарь morda-go работал локально:
```
➜ sudo mkdir -p /var/cache/geobase/
➜ sudo chown -R evbogdanov /var/cache
➜ scp v133.wdevx.yandex.net:/var/cache/geobase/geodata5.bin /var/cache/geobase/geodata5.bin
➜ scp v133.wdevx.yandex.net:/usr/share/yandex/lang_detect_data.txt /var/cache/lang_detect_data.txt
```
В файле `portal/avocado/libs/utils/langdetect/langdetect.go` поправить путь до `lang_detect_data.txt`
Исправить на `/var/cache/lang_detect_data.txt`
(положить файл по пути `/usr/share/yandex/` в MacOS невозможно)


Сборка и запуск:
```
➜ ya make -j 32 && cmd/morda-go/morda-go -config avocado.yaml
```

Отправка запросов - указывать именем бекенда девстенд
```
curl 'https://portal-hamster.yandex.ru/?srcrwr=MORDA__MORDA_GO_BACKEND%3Amorda-dev-v133.vla.yp-c.yandex.net%3A20400
```

Profit!