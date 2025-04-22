# Disk Volume Requests

Disk Volume Requests позволяют задавать дисковые ресурсы для пода.

{% note warning %}

Не факт, что поды будут выделятся ровно того размера, что вы заказали, sidecar (logbroker/tvm/juggler) добавляют налог на инфраструктуру сверх вашего текущего заказа.

{% endnote %}

Также, ко всем подам добавляется `1 GB` дискового места для инфраструктуры `pod_agent`.

Представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/data_model.proto?rev=6985827#L1178-1218):

## Как задать ресурсы через dctl {#dctl}

Почти во всех случаев достаточно заказывать ресурсы через `TQuotaPolicy`.

Стандартный заказ ресурсов выглядит примерно вот так:

```yaml
disk_volume_requests:
- id: id-is-not-important-just-random-string
  labels:
    used_by_infra: true
  quota_policy:
    bandwidth_guarantee: 1048576
    bandwidth_limit: 2097152
    capacity: 3221225472
  storage_class: hdd
```

Тут заказано `3 GB` диска, `1 MB / second` гарантии по `io` и стоит `2 MB / second` лимита по `io`
Тип заказанного диска `hdd`.

Можно заметить, что тут выставлен лейбл `used_by_infra`, важность этого флага объяснена ниже.
В случае, если в вашем заказе находится ровно один диск, то вам обязательно надо указать этот лейбл.

## Как задать ресурсы в UI {#ui}

При заказе подов в UI настройки диска указываются в общих настройках `deploy_unit`.

Для `hdd` `bandwidth_limit = 2 * bandwidth_guarantee`, для `ssd` `bandwidth_limit` выставляется равным `bandwidth_guarantee`.

## Что происходит, когда заказан один диск {#one_disk}

Тут описано поведение, которое будет после релиза [https://clubs.at.yandex-team.ru/infra-cloud/1074](https://clubs.at.yandex-team.ru/infra-cloud/1074)

То поведение, которые было до этого, является `deprecated`, и на него не надо полагаться.

Поведение для одного диска отличается от поведения для двух и более дисков из-за особенностей миграции на новую схему, в которой `pod_agent` и `sidecar box` изолированы по диску.

Если в заказе пользователя указан ровно один диск, то на этом диске **обязан** стоять флаг `used_by_infra: true`.

Далее заказ пользователя будет наполнен дополнительными дисковыми аллокациями для `pod_agent`, `logbroker` (если он задан в спеке) и `tvm` (если он задан в спеке).

Иными словами, из заказа вида:

```yaml
disk_volume_requests:
- id: random_id
  labels:
    used_by_infra: true
  quota_policy:
    capacity: 5097152000
  storage_class: hdd
```

При включенном `logbroker` мы получим заказ вида:

```yaml
disk_volume_requests:
- id: random_id
  labels:
    mount_path: /
    volume_type: root_fs
  quota_policy:
    capacity: 5097152000
  storage_class: hdd
- id: pod_agent
  labels:
    used_by_infra: true
  quota_policy:
    capacity: 1073741824
  storage_class: hdd
- id: logbroker
  quota_policy:
    capacity: 3221225472
  storage_class: hdd
```

`storage_class` у дополнительных дисков в данном случае равен `storage_class` единственного диска из спеки. Это сделано для того, чтобы при миграции со старой схемы (где просто увеличивали квоту в единственном заказанном диске) не возникало проблем с нехваткой квоты в аккаунтах. Например, есть аккаунты, где выделена только `ssd` квота, а `hdd` квота пустая.

`mount_path`, `volume_type` нужно для yp light, для первой итерации LVM'ов. Сейчас используются только для спец ручек мониторингов. 

`used_by_infra` - пережиток прошлого, для нодового агента данный тег означает, что на этом диске будет располагаться под агент. И при использовании дисковой изоляции(почти все стейджи переехали на использование этого) на уровне stage ctl этот лейбл снимается с диска пользователя и ставится на диск с под агентом. На текущий момент выставление этого лейбла от пользователя обязательно, так как хотим на уровне UI брать из диска с этим лейблом дефолты storage классов(если не указано явно в спеке) для сайдкар дисков.

`virtual_disk_id_ref` - id пользовательского диска, на котором будут хранится все данные объекта типа box/static_resource/layer/volume. 

В случае наличия одного диска вам никак не надо указывать `virtual_disk_id_ref` у объектов в спеке `pod_agent`, `stage controller` это сделает за вас.

### Что происходит, когда заказано более одного диска {#two_or_more_disks}

В данный момент деплой позволяет заказывать два и более диска через dctl. Id дисков не могут совпадать со значениями: `pod_agent`, `tvm` и `logbroker`. Данные идентификаторы зарезервированы нашей инфраструктурой под диски для сайдкаров.

{% note warning %}

Использование нескольких дисков невозможно, пока на вашем стейдже не включен механизм изоляции по дисковой квоте, те в вашей спеке присутствует лейбл `disable-disk-isolation-spi-15289`!!

{% endnote %}

### Пример спеки с использованием нескольких дисков

```yaml
spec:
  account_id: 'abc:service:3494'  # need replace: abc service id
  deploy_units:
    multiple_disks_example:  # need replace
      logbroker_config:
        logs_virtual_disk_id_ref: disk_1
        sidecar_volume:
          storage_class: 'hdd'
      coredump_config:
        test_workload:
          coredump_processor:
            probability: 100
            count_limit: 2
            total_size_limit_megabytes: 100
            aggregator:
              enabled: true
              url: https://coredumps.yandex-team.ru/submit_core
            volume_id: coredump_volume_id
      tvm_config:
        blackbox_environment: "ProdYaTeam"
        clients:
          - destinations:
              - alias: "to"
                app_id: 2022996
            secret_selector:
              alias: <secret_id>:<secret_version>
              id: 'client_secret'
            source:
              alias: "from"
              app_id: 2022996
        mode: "enabled"
        sidecar_volume:
          storage_class: 'hdd'
      multi_cluster_replica_set:
        replica_set:
          revision: 5
          deployment_strategy:
            max_unavailable: 2
          clusters:
            - cluster: 'sas'
              spec:
                replica_count: 1
          pod_template_spec:
            spec:
              secrets:
               ...
              disk_volume_requests:
                - id: 'disk_0'
                  storage_class: 'ssd'
                  quota_policy:
                    capacity: 2097152000
                    bandwidth_guarantee: 15728640
                    bandwidth_limit: 31457280
                  labels:
                    used_by_infra: TRUE
                    volume_type: 'root_fs'
                    mount_path: '/'
                - id: 'disk_1'
                  storage_class: 'hdd'
                  quota_policy:
                    capacity: 2097152000
              pod_agent_payload:
                meta:
                  sidecar_volume:
                    storage_class: 'ssd'
                spec:
                  resources:
                    layers:
                      - id: 'base_layer'
                        checksum: 'EMPTY:'
                        url: 'rbtorrent:edd2795d2d7674eae43c4ad0de3dad563be11f94'
                        virtual_disk_id_ref: 'disk_0'
                      - id: 'another_layer'
                        checksum: 'EMPTY:'
                        url: 'rbtorrent:d57bb5d384702469a420e497ac67d8c14986277f'
                        virtual_disk_id_ref: 'disk_1'
                    static_resources:
                      - id: 'my_resource'
                        verification:
                          checksum: 'EMPTY:'
                        url: 'rbtorrent:edd2795d2d7674eae43c4ad0de3dad563be11f94'
                        virtual_disk_id_ref: 'disk_1'
                  volumes:
                    - generic: {}
                      id: 'coredump_volume_id'
                      virtual_disk_id_ref: disk_0
                  workloads:
                    - id: 'test_workload'
                      transmit_logs: true
                      start:
                        command_line: "bash -c 'while :\ndo\necho log_string_1 >> /logs/log.txt \nsleep 1\ndone'"
                      box_ref: 'base_box'
                  mutable_workloads:
                    - workload_ref: 'test_workload'
                      target_state: 'active'
                  boxes:
                    - id: 'base_box'
                      rootfs:
                        layer_refs:
                          - 'base_layer'
                      virtual_disk_id_ref: 'disk_0'
                      volumes:
                        - mount_point: /coredumps
                          volume_ref: 'coredump_volume_id'
                          mode: read_write
                    - id: 'another_box'
                      rootfs:
                        layer_refs:
                          - 'another_layer'
                      virtual_disk_id_ref: 'disk_1'
                      static_resources:
                        - resource_ref: 'my_resource'
                          mount_point: '/my_res'
```

Для под агента, логброкера и tvm нашей инфраструктурой создаются отдельные диски.

### Дополнения для pod agent

```yaml
pod_agent_payload:
  meta:
    sidecar_volume:
      storage_class: 'ssd'
```

В случае использования нескольких дисков обязательно нужно указывать тип сторедж класса диска для под агента - ssd или hdd. В противном случае спека не пройдет валидацию.

### Дополнения для logbroker

```yaml
logbroker_config:
  logs_virtual_disk_id_ref: disk_1
  sidecar_volume:
    storage_class: 'hdd'
```

В случае использования нескольких дисков и отгрузки логов через логброкер обязательно нужно указывать:

- тип сторедж класса диска для логброкер сайдкара - ssd или hdd:

```yaml
sidecar_volume:
  storage_class: 'hdd
```

* id пользовательского диска, на котором будет размещен персистентный вольюм с порто лог файлами:

```yaml
logs_virtual_disk_id_ref: disk_1
```

Без вышеописанных двух пунктов спека не пройдет валидацию.

### Дополнения для tvm

```yaml
tvm_config:
  blackbox_environment: "ProdYaTeam"
  clients:
  - destinations:
    - alias: "to"
      app_id: 2022996
      secret_selector:
        alias: <secret_id>:<secret_version>
        id: 'client_secret'
        source:
          alias: "from"
          app_id: 2022996
   mode: "enabled"
   sidecar_volume:
     storage_class: 'hdd'
```

В случае использования нескольких дисков и tvm обязательно нужно указывать тип сторедж класса диска для tvm сайдкара - ssd или hdd, в противном случае спека не пройдет валидацию:

```yaml
sidecar_volume:
  storage_class: 'hdd'
```

### Дополнения для корок

```yaml
coredump_processor:
  probability: 100
  count_limit: 2
  total_size_limit_megabytes: 100
  aggregator:
    enabled: true
    url: https://coredumps.yandex-team.ru/submit_core
    volume_id: coredump_volume_id
```

Чтобы задать, на каком пользовательском диске будут располагаться корки, необходимо указать id персистентного вольюма для корок (опция не обязательна, если ее нету, то корки будут располагаться на дефолтном персистентном вольюме на том же диске пользователя, где и бокс):

```yaml
volume_id: coredump_volume_id
```

У вольюма в описании указываем реф на нужный диск:

```yaml
volumes:
- generic: {}
  id: 'coredump_volume_id'
  virtual_disk_id_ref: disk_1
```

### Дополнения для всего остального

Если используются несколько дисков, то для лееров, вольюмов, статических ресурсов и боксов необходимо указывать `virtual_disk_id_ref` пользовательского диска, на котором будут располагаться данные этих сущностей. В случае отстутствия этих рефов спека не пройдет валидацию.
Если бокс зависит от какого-то леера и статического ресурса, то все эти три сущности должны иметь одно и то же значение `virtual_disk_id_ref`.
