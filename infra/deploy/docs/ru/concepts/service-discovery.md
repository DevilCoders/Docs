# Service discovery

Service Discovery - это способ для сторонних систем (генераторов конфигов, балансеров, метапоисков и т.д.) обнаруживать в real-time бекенды.

Yandex.Deploy предоставляет две возможности для Service Discovery:

1) (высокоуровневый) [Настроить балансер](../launch/balancing.md) и ходить через него. Балансер будет скрывать за собой взаимодействия с YP Service Discovery.
1) (низкоуровневый) Воспользоваться [YP Service Discovery](https://wiki.yandex-team.ru/yp/discovery/). Ниже описан жизненные циклы `endpoint`/`endpoint_set` под управлением Yandex.Deploy.

## Взаимодействие с YP Service Discovery {#YP Service Discovery interaction}
Service Discovery в Yandex.Deploy (YD) построен поверх [Service Discovery в YP](https://wiki.yandex-team.ru/yp/discovery/):

- YP предоставляет [объекты](https://wiki.yandex-team.ru/yp/discovery/#tochkipodkljuchenija) `endpoint` и `endpoint_set` и интерфейс для их чтения/записи:
`endpoint` - точка доступа, содержащая поля `fqdn/port/protocol/ipv6_address/ipv4_address` - указывает на активный процесс, живущий в `pod`;
`endpoint_set` - множество `endpoint`, принадлежащих одному `deploy_unit` в конкретном YP-кластере.
- YD (как платформа) управляет `endpoint_set`/`endpoint` над подами, принадлежащими YD

Таким образом, контроль (создание/удаление) над `endpoint` принадлежит YD.
Пользователь может использовать интерфейсы/библиотеки YP для чтения множества `endpoint` конкретного сервиса (`deploy_unit`'а).

### Как создать endpoint_set {#create endpoint_set}

`endpoint_set` автоматически создается для каждого `deploy_unit`. По дефолту `port=80`. Поле `protocol` не заполняется.

При удалении `deploy_unit` YD автоматически удалит его `endpoint_sets` и `endpoints`.

Подробнее на странице [deploy_unit](deploy-unit/deploy-unit.md).

### Алгоритм создания/удаления endpoint {#endpoint-lifecycle}

YD создает `endpoint` для каждого "готового" (ready) `pod`'а.
`pod` "готов" - если все его `workloads` успешно прошли `readiness_check`.

Кроме того, в `endpoint_set` есть конфиг `double liveness_limit_ratio (default: 0.35 для endpoint_sets, созданных через deploy_unit.endpoint_sets)`:

- YD гарантирует, что `endpoints_count >= ceil(liveness_limit_ratio * pods_count)`.
Где `endpoints_count` - количество `endpoint` в `endpoint_set`,
`pods_count` - количество `pod`'ов в `deploy_unit` в конкретном YP-кластере.
Эта логика позволяет не закрывать весь трафик при падении пользовательского `readiness_check` на всех `pod`'ах (в виду бага или флапа).
- Если `endpoints_count` меньше `ceil(liveness_limit_ratio * pods_count)`,
YD будет (в неопределенном порядке) создавать `endpoint` для "неготовых" `pod`'ов, пока `endpoints_count` не достигнет `ceil(liveness_limit_ratio * pods_count)`.
- Если `endpoints_count` больше `ceil(liveness_limit_ratio * pods_count)`,
YD будет (в неопределенном порядке) удалять `endpoint` "неготовых" `pod`'ов, пока `endpoints_count` не достигнет `ceil(liveness_limit_ratio * pods_count)`.

"Готовность" пода по мнению YD записывается в `bool endpoint.status/ready`.
С помощью этого поля можно уносить логику "активной балансировки" над `endpoint`'ами в верхние слои (например, в балансер).
Например, можно указать `liveness_limit_ratio=1.0` - тогда `endpoint` будет создан для каждого `pod`'а, независимо от его статуса.
В таком случае решать, куда слать/не слать трафик, можно на клиентском уровне.

### Пример чтения endpoint's через ya tool dctl / ya tool yp {#endpoints_read_example}

```bash
# yanddmi-test-stage.deploy_unit - имя endpoint_set
yanddmi@yanddmi-dev[~]:ya tool dctl list endpoint yanddmi-test-stage.deploy_unit
+---------+----+--------------------------------------+--------------------------------+------+------+
| Cluster | ID |                 FQDN                 |              IPv6              | port | IPv4 |
+---------+----+--------------------------------------+--------------------------------+------+------+
|   sas   |    | yctz25uyiim2yo4r.sas.yp-c.yandex.net | 2a02:6b8:c1c:484:0:696:6e40:0  |  80  |      |
|   vla   |    | nxubsev2yof7z7i4.vla.yp-c.yandex.net | 2a02:6b8:c1d:2ba0:0:696:56b0:0 |  80  |      |
|   man   |    | tadqrfro2eglqr7g.man.yp-c.yandex.net | 2a02:6b8:c0a:3324:0:696:2d84:0 |  80  |      |
+---------+----+--------------------------------------+--------------------------------+------+------+
```

```bash
# yanddmi-test-stage.deploy_unit - имя endpoint_set
yanddmi@yanddmi-dev[~]:ya tool yp select --address sas --filter '[/meta/endpoint_set_id]="yanddmi-test-stage.deploy_unit"' endpoint /spec /status
+------------------------------------------------------------------------------------------------------------------------+------------------+
|                                                         /spec                                                          |     /status      |
+------------------------------------------------------------------------------------------------------------------------+------------------+
| {"ip6_address"="2a02:6b8:c1c:484:0:696:6e40:0";"protocol"="";"fqdn"="yctz25uyiim2yo4r.sas.yp-c.yandex.net";"port"=80;} | {"ready"=%true;} |
+------------------------------------------------------------------------------------------------------------------------+------------------+
1 object(s) selected
```
