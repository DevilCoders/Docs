[Графики](https://monitoring.yandex-team.ru/projects/grad/dashboards/monhh0k0ont3p97l36ha?range=1h&refresh=60) \
Кондукторная группа [nocdev-gradc](https://c.yandex-team.ru/groups/nocdev-gradc) \
Конфиг [nocdev-grad-server.sls](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-gradc)

Опции SolomonPusher2(params):
```yaml
  solomon:
    url: http://solomon.yandex.net/api/v2/push
    protocol: solomon2
    max_concurrency: 50
    max_metrics: 10000
    instance_count: 5
    params:
      token: token
```

**token** - OAuth токен.\
**sensor_name_label** - Имя сенсора по [SOLOMON-3923](https://st.yandex-team.ru/SOLOMON-3923)
Запись метрик в UA:\
```yaml
internal_metrics_url: "http://olo:22132"  # URL Unified Agent \
internal_metrics_sensor: "sensor" # имя сенсора
```
Опции SolomonPusher2 в series:
```yaml
series:
  snmp_poller.snmp:
    client:
      solomon: { common_labels: { project: noc, cluster: cluster, service: svc } }
```
**host_hash** - Вычисление cluster из тега host. Поддерживается только значение sha1_last4.\
**common_labels** - project, cluster и service куда будут записаны данные.


## Метрики
##### client_collector
сенсор | Описание
--- | ---
in_qsize | Загруженность очереди получения данных из RMQ
out_qsize | Загруженность очереди в сторону писателей в соломон
out_qdrop | Количество удаленных данных из очереди

##### grad_client
сенсор | Описание
--- | ---
retry | Число перепосылок в соломон

### Деплой
Сама же аркадия заливает пакеты в unstable. В stable перенести можно так:
```shell
ssh noc.dupload.dist.yandex.ru
find_package -e unstable grad-client | grep _amd64.deb
sudo dmove noc stable grad-client 1.8.xxx unstable
```
Выкатка конфигов
```shell
executer p_exec %nocdev-gradc "salt-call state.highstate queue=True"
```

Выкатить пакет руками:
```shell
executer p_exec %grad_vs "apt-get update; apt-get install grad-client=1.8...."
```
