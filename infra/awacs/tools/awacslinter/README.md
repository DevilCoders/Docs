```
AWACS_TOKEN=AQAD-XXX \
../awacsls/awacsls ls --condition ALL | xargs -I % ./awacslinter check --namespace-id % --rule attempts
```
would print something like
```
"arl" rule warnings:
Balancer: vinsbot.alice.yandex.net/vinsbot.alice.yandex.net_man
Path: instance_macro -> admin
Message: Hey there, here are some IP addresses for you: 127.0.0.1 ::1
---
Balancer: vinsbot.alice.yandex.net/vinsbot.alice.yandex.net_man
Path: instance_macro -> http_section
Message: Hey there, here are some IP addresses for you: *
---
Balancer: vinsbot.alice.yandex.net/vinsbot.alice.yandex.net_man
Path: instance_macro -> http_section -> extended_http_macro -> regexp -> default -> balancer2
Message: This is a balancer2 with 3 branches: vins_bot_man, vins_bot_sas, vins_bot_vla
---
Balancer: vinsbot.alice.yandex.net/vinsbot.alice.yandex.net_man
Path: instance_macro -> http_section -> extended_http_macro -> regexp -> default -> balancer2 -> backends[2] -> report -> balancer2
Message: This is a balancer2 with 1 real instances and 0 endpoint sets, preceded by 1 balancer2 modules
---
Balancer: vinsbot.alice.yandex.net/vinsbot.alice.yandex.net_man
Path: instance_macro -> http_section -> extended_http_macro -> regexp -> default -> balancer2 -> backends[1] -> report -> balancer2
Message: This is a balancer2 with 2 real instances and 0 endpoint sets, preceded by 1 balancer2 modules
---
Balancer: vinsbot.alice.yandex.net/vinsbot.alice.yandex.net_man
Path: instance_macro -> http_section -> extended_http_macro -> regexp -> default -> balancer2 -> backends[0] -> report -> balancer2
Message: This is a balancer2 with 1 real instances and 0 endpoint sets, preceded by 1 balancer2 modules
---
...
```