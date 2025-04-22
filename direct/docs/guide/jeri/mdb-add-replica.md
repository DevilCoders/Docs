# Добавление реплики в текущие шарды MDB

## О назначении инструкции { #about }

Инструкция рассказывает какие действия требуется произвести, чтобы ввести в эксплуатацию новую реплику в уже работающем шарде.

### Подготовка

Нужна роль "Администратор MDB" в сервисе "Инфраструктура Директа" <https://abc.yandex-team.ru/services/direct_infra/>

### Алгоритм действий

#### Добавление хоста
1. Заходим в интрефейс MDB и выбираем интересующий шард. Состояние кластера должно быть "Alive".
2. Слева выбираем "Хосты". Откроется список реплик в текущем шарде.
3. Сверху справа будет кнопка "+ Добавить хост". Откроется менюшка с выбором локации.
4. После создания операции, стоит подождать 5 минут. Может случится ситуация, что указанной локации не будет места и операция будет отменена.
5. Если операция не была удалена и выполняется(слева кнопка "Операции"), переходим к добавлению нового хоста в конфиги

#### Изменение конфигов
- Добавляем новый хост в `"cluster_hosts"` в `db-config`.  
⚠️ Важно это делать сразу, т.к. после наливки новая машина может стать мастером. `direct-mmm` не сможет обновить конфиг, если не будет о ней знать
```
ppcback01f:# direct-db-config -e
```

{% cut "Подробнее" %}

`direct-db-config` — это alias для `zk-db-config -t dbtools_direct -c /etc/zk-delivery/ppc.cfg -n /direct/db-config.json -e`

Например, так будет выглядеть конфиг 8 шарда после добавления реплики `vla-wgrx4n6qbrvthlj5.db.yandex.net`:
```
"8": {
 "cluster_hosts": "iva-acd0zc9vnm509a67.db.yandex.net,sas-z6imjtad43gzlb8s.db.yandex.net,vla-wgrx4n6qbrvthlj5.db.yandex.net",
 "host": "iva-acd0zc9vnm509a67.db.yandex.net",
 "instance": "ppcdata8",
 "port": 3306,
 "weight": 1
}
```

{% endcut %}

После добавления стоит проверить, что `direct-mmm` увидел новую реплику и добавил её в правильную группу. В логах должна появиться соответствующая запись

{% cut "Пример" %}

В логах несколько сообщений вида: 
<https://direct.yandex.ru/logviewer/short/v2/2239123865398833200>
```
add host man-b397grvb926ms5yk.db.yandex.net to group ppcdata13
```

{% endcut %}

- Обновляем конфиг `alldb-config.json` ([direct/infra/direct-utils/zk-sync/confs/alldb-config.json](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/zk-sync/confs/alldb-config.json)).  
Новую машину требуется добавить в секцию `"replicas"` соответствующего шарда.  

{% cut "Пример" %}

```
            "replicas": [
                {
                    "host": "vla-wgrx4n6qbrvthlj5.db.yandex.net",
                    "dc": "vla",
                    "mysql_port": 3306,
                    "switchover_weight": 3,
                    "maintenance": false
                },
            ]
```

{% endcut %}

От этого конфига завит работа db_availible мониторинга. Если машины не окажется в нем, она будет вне зоны видимости мониторинга.

- directadmin-juggler можно обновить руками или подождать когда он обновится автоматически(раз в час)

{% cut "Пример" %}

```
ppcback01f:# sudo -u ppc directadmin-make-juggler.py --svn-path arcadia.yandex.ru/arc/trunk/arcadia/direct/infra/direct-utils/directadmin-juggler/checks --svn-user robot-direct-arc-p --svn-key /etc/direct-tokens/ssh-rsa_robot-direct-arc-p --check-first --apply --token /etc/direct-tokens/juggler_api -v -d
```

{% endcut %}

Некоторые мониторинги завязаны на ready_for_operation(живость хоста), который смотрит на кондукторную группу. При добавлении хоста в текущие шарды что-то явно делать тут не нужно, но следует через какое-то время проверить, что необходимые events начали отправляться в juggler.


### Мониторинг
- <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Ddirect.prod_ppcdata> - набор проверок над direct.prod_ppcdata
- <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Ddirect.prod_ppcdata.db_mdbd7g2o0jiipju186pq> - для ppcdata19. При необходимости подставь ID нужного инстанса

### Ссылки { #links }

- mysql-master-monitor: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-master-monitor>
