# Вопросы о планировщиках ресурсов (YP/GENCFG)
## PORTO_CONSTRAINTS_ERROR {#porto_constraints_error}
PORTO_CONSTRAINTS_ERROR обычно означает, что превышены гарантии по памяти на хосте. Кто-то не съехал и занимает память.
Утверждается, что GENCFG умеет генерить топологии с учётом активных инстансов на хостах, поэтому подобной проблемы возникать не должно. Если же это случилось, следовательно, что-то пошло не так, как утверждается, и об этом следует сообщить в [gencfg](https://h.yandex-team.ru/?https%3A%2F%2Ft.me%2Fjoinchat%2FBlz_uD9XGMHGSqjiPlFXVw).
Так же данная проблема может быть связана с тем, что у сервиса переопределены лимиты в Nanny.
Диагностировать данную проблему, найти сервис инстанс, которого должен отсутствовать в новой топологии кластера, можно следующими способами:
- Простой способ воспользоваться [https://gencfg.yandex-team.ru/extra_groups/](https://gencfg.yandex-team.ru/extra_groups/) данная форма покажет, какой сервис на указанном хосте лишний.
- Если данный способ не помог и были переопределены лимиты то вы можете воспользоваться скриптом [wabbajack](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/wabbajack/Wabbajack-Install-guide/?from=%252Fjandekspoisk%252Fsepe%252Fdezhurnajasmena%252Fwabbajack%252Fwabbajack-servis-avtomaticheskogo-sbora-diagnostiki%252FWabbajack-Install-guide%252F) checks.run

```
checks.run check=GencfgTopologyDiff args='{"host":"<hostname>", "gencfg_last_tag":"<last_gencfg_tag>"}'
```

Так же PORTO_CONSTRAINTS_ERROR может возникать при overcommit по cpu при этом роль тут играет не только распределение cpu грантии, но и cpu_set/affinity. Более подробно можно прочитать в контексте тикета [RTCSUPPORT-5008](https://st.yandex-team.ru/RTCSUPPORT-3845).

## YP Service Discovery {#yp_service_discovery}
Для сервиса в YP правильно получать список инстансов с помощью [Service Discovery](https://wiki.yandex-team.ru/yp/yp-quick-start-guide/#yp.sd).
Этот запрос правильнее отправлять в специально выделенный для этого сервис - sd.yandex.net. Такие запросы не требуют авторизации, в отличие от запросов в YP напрямую.
Используйте корректный client_name в запросах - это позволит связаться с вами, если что-то вдруг пойдёт не так.

{% cut "Пример получения адресов для всех ДЦ" %}

```bash
endpoint_set_id='wabbajack'
client_id='naumbi4'
for cn in iva myt sas man vla ; do curl -s "http://sd.yandex.net:8080/resolve_endpoints/json" --data '{"cluster_name": "'"${cn}"'", "endpoint_set_id": "'"${endpoint_set_id}"'", "client_name": "'"${client_id}"'"}' | jq -c '{"'"${cn}"'": .endpoint_set.endpoints}' ; done | jq -sr '. | add | map(. | values) | add | map("http://" + .fqdn + ":" + (.port | tostring))[]'
```

{% endcut %}

{% cut "Пример ответа" %}

```(json)
http://i2sh46shkcymfi2f.sas.yp-c.yandex.net:80
http://insu5xcwurxdt57o.sas.yp-c.yandex.net:80
http://d7oyqlth5fzkcf5o.sas.yp-c.yandex.net:80
http://wcsbtote2q5hxbhu.man.yp-c.yandex.net:80
http://hvtjodwg5eyivept.man.yp-c.yandex.net:80
http://kqykdursumsnxe3q.man.yp-c.yandex.net:80
http://gpac6q7kxdv5sbb4.vla.yp-c.yandex.net:80
http://t5lwbpdqm2xh7mq7.vla.yp-c.yandex.net:80
http://rdoshf2rywo3fdzh.vla.yp-c.yandex.net:80
```
Подробнее формат ответа описан в [документации YP](https://wiki.yandex-team.ru/yp/yp-quick-start-guide/#yp.sd).

{% endcut %}

## Сожительство YP и GenCFG {#cohabitation}
Не все сервисы в GenCFG изолированы, поэтому на таких нодах могут быть проблемы со свободным местом, например.
Проверить, что под попал на такую ноду, можно так:

```
$ ya tool yp_util pod neighbours wzzzifmtuxglwect --cluster sas
╒════╤══════════════════════════════════════════════════╤══════════════════════════════════════════════════════════════════════════╕
│    │ Neighbours on node sas3-5990.search.yandex.net   │ On host with not isolated Gencfg containers=True                         │
╞════╪══════════════════════════════════════════════════╪══════════════════════════════════════════════════════════════════════════╡
│  0 │ wzzzifmtuxglwect                                 │ https://nanny.yandex-team.ru/ui/#/services/catalog/infra_monitoring_sas/ │
╘════╧══════════════════════════════════════════════════╧══════════════════════════════════════════════════════════════════════════╛
```

Обращать внимание на надпись `On host with not isolated Gencfg containers=True`
На самом хосте можно проверять "трёхголовость" ISS-агента - его источники данных.
На хосте в режиме сожительства будет так:

```
cat /place/db/iss3/application.conf | jq '.agent.hostConfiguration | ((.providersNumber > 1) and .ypProvider.enabled)'
true
```

## Форсированная эвакуация пода YP с хоста. {#eviction}
**Права на данную операцию есть у ограниченного количества человек! Если вам по какой-то причине потребовалось эвакуировать под - обратитесь в [чат](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q) поддержки RTCSUPPORT.**
Запрос на эвакуацию производится с помощью комманды утилиты yp или прямо из интерфейса систем деплоя.

```
yp request-pod-eviction <pod_id> "<описание причины передвижения>, лучше всего тикет из ST" --address <cluster name>
```
После чего проверить, что запрос на выселение появился в YP.

```
yp get <pod_id> --address <cluster name> --selector /status/eviction
```
Должно вывестись requested и сообщение, которое добавляли в качестве обоснования. Пример:

```
ya tools yp get pod kawmawbjnl2lqhwa --address sas --selector /status/eviction
[
    {
        "state" = "requested";
        "message" = "Checking eviction by request from A. Dmitriyev";
        "last_updated" = 1578584396512314u;
        "reason" = "client";
    };
]
```

После чего будет запущена политика репликации в nanny-сервисе пода.

## История переезда пода в YP. {#select-object-history}

Историю по переездам пода можно глянуть с помощью ya tool yp:

```
YP_ADDRESS=sas ya tool yp select-object-history pod ff55gje5a6pkhmel --selector /status/eviction --prettify-events
```

## Как найти сервис по IP в YP. {#pod-by-ip}

```
$ host 2a02:6b8:c08:b018:0:409b:c4b8:0
0.0.0.0.8.b.4.c.b.9.0.4.0.0.0.0.8.1.0.b.8.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa domain name pointer rb4oklvci6bo623n.sas.yp-c.yandex.net.
$ YP_ADDRESS=sas ya tool yp get pod rb4oklvci6bo623n /labels
[
    {
        "nanny_version" = "43694ca9-6d94-497e-b612-64945a718cd8";
        "hq_synced_eviction_time" = "1598517933751321";
        "nanny_service_id" = "rtc_balancer_spec-promo-external_yandex_net_sas";
        "last_eviction_time" = "1596631138";
        "deploy_engine" = "YP_LITE";
    };
]
```

Если получаете ошибку NXDOMAIN то имеет смысл заменить `:0` в конце на `:1`:
```
➜  ~ host 2a02:6b8:c0b:6a23:0:484c:6436:0
Host 0.0.0.0.6.3.4.6.c.4.8.4.0.0.0.0.3.2.a.6.b.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa not found: 3(NXDOMAIN)
➜  ~ host 2a02:6b8:c0b:6a23:0:484c:6436:1
1.0.0.0.6.3.4.6.c.4.8.4.0.0.0.0.3.2.a.6.b.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa domain name pointer gente-box.rrthqykbwxnbcxcr.man.yp-c.yandex.net.
```
