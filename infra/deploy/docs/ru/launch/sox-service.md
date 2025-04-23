## Описание

Для прохождения сервисом аудита (PCI DSS или SOX) он должен соответствовать следующим требованиям:
1. Изоляция между боксами, то есть из подконтейнера бокса невозможно делать никаких write действий через порто апи с контейнерами и подконтейнерами соседних боксов. Для этого на стороне под агента реализована возможность запускать бокс в режиме child-only
2. Невозможность получения значений переменных с секретами через порто апи при запросе portoctl get у контейнера. Реализуется путем приноса переменных  с секретами в контейнеры через secret_env. 
3. Отсутствие доступа к файлам с секретам сервиса со стороны пользователя nobody, для этого на стороне под агента сделана функциональность по установке прав доступа на статические ресурсы
4. Защита от подмены критичных данных сервиса, а именно бинарных файлов и конфигов. Есть два способа достижения этого: 
   * На стороне подового агента есть возможность приносить слои и статические ресурсы в volume, монтируемый к боксу как read only.
   * На стороне под агента реализована возможность запускать пользовательский бокс с read only rootfs.
**Примечание**. Второй способ более сложен во внедрении, так как при read only rootfs нужно делать необходимые сервису папки как writable путем монтирования в них writable вольюмов (доступно через UI).

Вся вышеописанная функциональность доступна с версии под агента, начиная с [101-1](https://deploy.yandex-team.ru/docs/reference/pod-agent-releases#:0) и [runtime revision 7](../reference/patchers-revision#runtime-version-7) или выше. Функциональность из пунктов 1, 2 включается автоматически в случае выставления на деплой юните флага `sox_service: true` и использовании runtime revision 7 или выше. Функциональность из пунктов 3, 4 включается отдельными настройками в сервисе. Также при выставлении флага `sox_service: true` на деплой юните становится возможным заходить в пользовательский бокс под пользователем nobody, у которого ограничены привилегии, а именно `no capabilities, no porto, virt_mode=app`.  При выполнении всех условий, в случае захода в бокс под nobody не будут генерироваться SECALERTS.

Ниже приведены примеры настроек сервиса, а также описание настроек и деталей реализации.

## Примеры донастроек безопасности сервиса, проходящего аудит
Ниже приведены два примера настройки сервиса для прохождения аудита.
Примеры отличаются различной подготовкой файловой системы внутри боксов контейнера:
* в первом случае пользователь делает volume, в который приносятся пользовательские ресурсы, для защиты от их модификации. Данный вольюм монтируется к пользовательскому боксу как read only.
* во втором способе создается readonly rootfs бокса, куда подмонтируются вольюмы для изменяемых файлов - логов, корок и т п.
В части остальных настроек оба способа идентичны.

### Способ 1. Принос слоев и статических ресурсов в volume, монтируемый к пользовательскому боксу как read only. 
![image](https://jing.yandex-team.ru/files/amich/RO%20mount.png).

**Пример спеки с приносом слоев и статических ресурсов в volume, монтируемый к пользовательскому боксу как read only, режимом child-only для пользовательского бокса, secret env для переменных с секретами и правами доступа на файлы с секретами**

{% cut "Пример спецификации" %}

```
1   spec:
2     account_id: abc:service:3494
3     deploy_units:
4       security_features_deploy_unit:
5         sox_service: true
6         patchers_revision: 11
7         multi_cluster_replica_set:
8           replica_set:
9             account_id: tmp
10            clusters:
11            - cluster: sas-test
12              spec:
13                replica_count: 1
14            deployment_strategy:
15              max_unavailable: 2
16            pod_template_spec:
17              spec:
18                disk_volume_requests:
19                - id: root
20                  labels:
21                    mount_path: /
22                    used_by_infra: true
23                    volume_type: root_fs
24                  quota_policy:
25                    capacity: 5097152000
26                  storage_class: hdd
27                ip6_address_requests:
28                - enable_dns: true
29                  network_id: _SEARCHSAND_
30                  vlan_id: backbone
31                - enable_dns: true
32                  network_id: _SEARCHSAND_
33                  vlan_id: fastbone
34                pod_agent_payload:
35                  spec:
36                    boxes:
37                    - id: base_box
38                      rootfs:
39                        layer_refs:
40                        - base_layer
41                      static_resources:
42                      - mount_point: tokens1
43                        resource_ref: "tokens"
44                      volumes:
45                      - mount_point: /app/bin
46                        volume_ref: readonly_volume
47                        mode: 'read_only'                   
48                    mutable_workloads:
49                    - workload_ref: server6_workload
50                    volumes:
51                    - id: readonly_volume
52                      generic:
53                        layer_refs:
54                        - simple_http_server
55                      static_resources:
56                      - resource_ref: 'configs'
57                        volume_relative_mount_point: /configs
58                    resources:
59                      layers:
60                      - checksum: 'EMPTY:'
61                        id: base_layer
62                        url: rbtorrent:49969bbdbc58134227a8e3276e92d843f0f904b2
63                      - checksum: 'EMPTY:'
64                        id: simple_http_server
65                        url: rbtorrent:d57bb5d384702469a420e497ac67d8c14986277f
66                      static_resources:
67                      - access_permissions: '600'
68                        files:
69                          files:
70                          - file_name: yp_token
71                            secret_data:
72                              alias: '<secret_id>:<secret_ver>'
73                              id: yp-token
74                        id: 'tokens'
75                        verification:
76                          check_period_ms: 60000
77                          checksum: 'EMPTY:'
78                      - id: 'configs'
79                        url: rbtorrent:d6ff1ef09586db9c02ef4352f72f0b736b9c33e7
80                        verification:
81                          check_period_ms: 10000
82                          checksum: 'EMPTY:'
83                    workloads:
84                    - box_ref: base_box
85                      id: server6_workload
86                      transmit_logs: true
87                      readiness_check:
88                        container:
89                          command_line: /bin/bash -c true
90                          time_limit:
91                            initial_delay_ms: 1000
92                            max_execution_time_ms: 300000
93                            max_restart_period_ms: 60000
94                            min_restart_period_ms: 60000
95                            restart_period_back_off: 1
96                            restart_period_scale_ms: 1
97                      start:
98                        command_line: 'bash -c '/app/bin/simple_http_server 80 'Hello my dear @dkochetov!' > /var/log/server_out''
99                resource_requests:
100                 memory_guarantee: 322122542
101                 memory_limit: 322122542
102                 vcpu_guarantee: 400
103                 vcpu_limit: 400
104               secrets:
105                 <secret_id>:<secret_ver>:
106                   delegation_token: <token>
107                   secret_id: <secret_id>
108                   secret_version: <secret_ver>
109           revision: 1
110       network_defaults:
111         network_id: _SEARCHSAND_
112       revision: 1
113   revision: 1

```

**Что было добавлено:**
1. Строка 63 - 65 слой с бинарными файлами, которые необходимо сделать read only
    
    ```yaml
    - checksum: 'EMPTY:'
      id: simple_http_server
      url: rbtorrent:d57bb5d384702469a420e497ac67d8c14986277f
    ```

2. Cтроки 50 - 57, 44 - 47, создаем вольюм, который внутри себя будет содержать лейр simple_http_server и статический ресурс configs, монтируем этот вольюм в rootfs пользовательского бокса как read only в папку /app/bin. В итоге, в данной папке появятся файлы из лейра base_layer_1 и статического ресурса configs. /app/bin будет read only. Более подробно [тут](sox-service#vozmozhnostь-prinositь-sloi-i-staticheskie-resursy-v-volume,-montiruemyj-k-boksu-kak-read-only)

    ```yaml
    volumes:
    - id: readonly_volume
      generic:
        layer_refs:
        - simple_http_server
      static_resources:
      - resource_ref: 'configs'
        volume_relative_mount_point: /configs
    ```
    ```yaml
    volumes:
    - mount_point: /app/bin
      volume_ref: readonly_volume
      mode: 'read_only'
    ```

3. Строка 5 и 6 выставляем для сервиса рантайм версию 11 (актуальная на момент написания документации) и выставляем флаг, что это сокс сервис. При этих флагах пользовательские боксы начинают запускаться с режимом [child-only](#child-only), все переменные с секретами начинают приноситься через [secret_env](#secret-env-get). 
    
    ```yaml
    sox_service: true
    patchers_revision: 11
    ```

4. Строка 67 — выставляем [права доступа на статический ресурс](sox-service#ustanovka-sekьyurnyh-prav-na-staticheskie-resursy) с секретом yp_token, чтоб он был невиден пользователю nobody.
    
    ```yaml
    access_permissions: '600'
    ```

5. Строка 97 — 98 в старт команде ворклоуда используется бинарный файл для запуска из readonly_volume
    
    ```yaml
    start:
      command_line: 'bash -c '/app/bin/simple_http_server 80 'Hello my dear @dkochetov!' > /var/log/server_out''
    ```

{% endcut %}

Данный способ заведения сервиса под sox аудит предпочтительнее в случае, если для сервиса нет требования класть read only бинарные файлы в папку с уже существующими на рут фс системными файлами, к примеру в /bin, так как в случае монтирования вольюма в /bin все изначально существующие в ней системные файлы будут невидны для системы.
В случае использования в сервисе докер образов вышеописанный способ заведения сервиса под sox аудит применяется аналогично.

### Способ 2. Read only box rootfs
![image](https://jing.yandex-team.ru/files/amich/RW%20volume.png).



**Пример спеки с read only box rootfs, режимом child-only для пользовательского бокса, secret env для переменных с секретами и правами доступа на файлы с секретами.**

{% cut "Пример спецификации" %}


```
1    spec:
2      account_id: abc:service:3494
3      deploy_units:
4        security_features_deploy_unit:
5          box_juggler_configs:
6            base_box:
7              port: 31580
8          coredump_config:
9            server6_workload:
10             coredump_processor:
11               count_limit: 3
12               probability: 100
13               total_size_limit_megabytes: 1024
14         logrotate_configs:
15           base_box:
16             run_period_millisecond: 60000
17         network_defaults:
18           network_id: _SEARCHSAND_
19         sox_service: true
20         patchers_revision: 11
21         replica_set:
22           per_cluster_settings:
23             sas:
24               deployment_strategy:
25                 max_unavailable: 1
26               pod_count: 1
27           replica_set_template:
28             constraints:
29               antiaffinity_constraints:
30               - key: rack
31                 max_pods: 1
32             pod_template_spec:
33               spec:
34                 disk_volume_requests:
35                 - id: root
36                   labels:
37                     mount_path: /
38                     used_by_infra: true
39                     volume_type: root_fs
40                   quota_policy:
41                     capacity: 5097152000
42                   storage_class: hdd
43                ip6_address_requests:
44                - enable_dns: true
45                  network_id: _SEARCHSAND_
46                  vlan_id: backbone
47                - enable_dns: true
48                  network_id: _SEARCHSAND_
49                  vlan_id: "fastbone"
50              pod_agent_payload:
51                spec:
52                  boxes:
53                  - id: base_box
54                    rootfs:
55                      create_mode: read_only
56                      layer_refs:
57                      - base_layer
58                      - simple_http_server
59                    static_resources:
60                    - mount_point: tokens1
61                      resource_ref: tokens
62                    volumes:
63                    - mode: read_write
64                      mount_point: /var/log
65                      volume_ref: writable_volume
66                  mutable_workloads:
67                  - workload_ref: server6_workload
68                  resources:
69                    layers:
70                    - checksum: 'EMPTY:'
71                      id: base_layer
72                      url: rbtorrent:49969bbdbc58134227a8e3276e92d843f0f904b2
73                    - checksum: 'EMPTY:'
74                      id: simple_http_server
75                      url: rbtorrent:d57bb5d384702469a420e497ac67d8c14986277f
76                  static_resources:
77                  - access_permissions: '600'
78                    files:
79                      files:
80                      - file_name: "yp_token"
81                        secret_data:
82                          alias: '<secret_id>:<secret_ver>'
83                          id: "yp-token"
84                      id: tokens
85                      verification:
86                        check_period_ms: 60000
87                        checksum: 'EMPTY:'
88                  volumes:
89                  - generic: {}
90                    id: writable_volume
91                    persistence_type: non_persistent
92                  workloads:
93                  - box_ref: base_box
94                    env:
95                    - name: YP_TOKEN
96                      value:
97                        secret_env:
98                          alias: '<secret_id>:<secret_ver>'
99                          id: yp-token
100                   id: server6_workload
101                   readiness_check:
102                     container:
103                       command_line: /bin/bash -c true
104                       time_limit:
105                         initial_delay_ms: 1000
106                         max_execution_time_ms: 300000
107                         max_restart_period_ms: 60000
108                         min_restart_period_ms: 60000
109                         restart_period_back_off: 1
110                         restart_period_scale_ms: 1
111                   start:
112                     command_line: 'bash -c '/simple_http_server 80 'Hello my dear @dkochetov!' > /var/log/server_out''
113                   transmit_logs: true
114             resource_requests:
115               memory_guarantee: 322122548
116               memory_limit: 322122548
117               vcpu_guarantee: 200
118               vcpu_limit: 200
119             secrets:
120               <secret_id>:<secret_ver>:
121                 delegation_token: <token>
122                 secret_id: <secret_id>
123                 secret_version: <secret_ver>
124     revision: 4
125 revision: 4
126 revision_info:
127   description: null
```


**Что было добавлено:**
1. Строка 73 - 75 слой с бинарными файлами, которыми необходимо сделать read only

    ```yaml
    - checksum: 'EMPTY:'
      id: simple_http_server
      url: rbtorrent:d57bb5d384702469a420e497ac67d8c14986277f
    ```

2. Cтрока 55, делаем [rootfs пользовательского бокса как read only](sox-service#read-only-rootfs-dlya-kontejnerov-boksov).
    
    ```yaml
    create_mode: 'read_only'
    ```

3. Cтрока 88 - 91 и 62 - 65, делаем папку /var/log на рутфс бокса пользователя как writable при помощи монтирования к ней writable неперсистентного вольюма, эта папка нужна процессу ворклоуда как writable. В данном случае мы делаем вольюм неперсистентным, то есть он будет пересобираться в случае пересборки бокса, к которому он примонтирован. Неперсистентный вольюм может быть примонтирован только к одному боксу и только в одну точку монтирования.

    ```yaml
    volumes:
    - generic: {}
      id: writable_volume
      persistence_type: non_persistent
    ```

    ```yaml
    volumes:
      - mode: 'read_write'
        mount_point: /var/log
        volume_ref: writable_volume
    ```

    Про оснонвые особенности использования read only rootfs для боксов описано [тут](sox-service#read-only-rootfs-dlya-kontejnerov-boksov).


4. Строка 19 и 20 выставляем для сервиса рантайм версию 7 и выставляем флаг, что это сокс сервис. При этих флагах пользовательские боксы начинают запускаться с режимом [child-only](#child-only), все переменные с секретами начинают приноситься через [secret_env](#secret-env-get) и автоматом спека дообогащается всеми необходимыми папками и вольюмами для работы deploy системных сайдкаров с [read only box rootfs](sox-service.html#read-only-rootfs-dlya-kontejnerov-boksov) 
    
    ```yaml
    sox_service: true
    patchers_revision: 11
    ```

5. Cтрока 77 - выставляем [права доступа на статический ресурс](sox-service#ustanovka-sekьyurnyh-prav-na-staticheskie-resursy) с секретом yp_token, чтоб он был невиден пользователю nobody.
    
    ```yaml
    access_permissions: '600'
    ```

6. Строка 111 - 112 в старт команде ворклоуда используется бинарный файл для запуска из rootfs бокса
    
    ```yaml
    start:
      command_line: 'bash -c '/simple_http_server 80 'Hello my dear @dkochetov!' > /var/log/server_out''
     ```    

{% endcut %}


Данный способ заведения сервиса под sox аудит предпочтильнее в случае, если ваши рид онли бинарные файлы должны быть положены в папки с уже существующими системными файлами, к примеру в /bin.
В случае использования в сервисе докер образов вышеописанный способ заведения сервиса под sox аудит применяется аналогично.

## Запуск контейнеров боксов в режиме child-only {#child-only}

Если контейнер бокса запускается с режимом child-only, то процессы в подконтейнерах бокса не могут сделать write действий через порто с соседними для данного бокса контейнерами и их подконтейнерами.

{% cut "Пример работы" %}

```bash
dkochetov@sas1-8015:~$ portoctl  get ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box | grep enable_porto
enable_porto = child-only
dkochetov@sas1-8015:~$ sudo portoctl shell ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box
(ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box)root@pyqspjxmzks3gugc:/# portoctl list   
....
pod_agent                                                                          running     0:01:36
pod_agent_box_base_box                                                                meta     0:01:23
....
(ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box)root@pyqspjxmzks3gugc:/# portoctl destroy pod_agent
Can't destroy container: Permission:(Write access denied: container ISS-AGENT--pyqspjxmzks3gugc/pod_agent out of scope)
```

{% endcut %}

Из вышеописанного примера видно, что pod_agent_box_base_box запущен в режиме child-only. Шелл подконтейнер внутри pod_agent_box_base_box не может задестроить контейнер с под агентом.

Данная функциональность автоматом включается для сокс сервисов в случае использования runtime revision 7 и выше.

{% cut "Пример спецификации" %}

```yaml
deploy_units:
  security_features_deploy_unit:
....
    sox_service: true
    patchers_revision: 7

    replica_set:
.....
```
{% endcut %}

Пример полной спеки с режимом child-only для base_box [тут](sox-service#sposob-1-prinos-sloev-i-staticheskih-resursov-v-volume,-montiruemyj-k-polьzovatelьskomu-boksu-kak-read-only).


## Принос секретов через secret env {#secret-env-get}

В случае приноса секретов через secret env, переменные с секретами не будут видны при вызове portoctl get для контейнера.

{% cut "Пример работы" %}
```bash
dkochetov@sas1-8015:~$ portoctl get ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box/workload_server6_workload_start | grep env | grep YP_TOKEN
env_secret = YP_TOKEN=<secret salt=.... md5=....>
```
{% endcut %}

В вышеописанном примере переменная YP_TOKEN, содержащая секрет, приносится через secret env. Значение переменной невидно при вызове portoctl get для ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box/workload_server6_workload_start.

Данная функциональность автоматом включается для сокс сервисов в случае использования runtime revision 7 и выше:

{% cut "Пример спецификации" %}

```yaml
deploy_units:
  security_features_deploy_unit:
....
    sox_service: true
    patchers_revision: 7

    replica_set:
.....
```
{% endcut %}

Пример полной спеки с приносом yp_token через secret env [тут](sox-service#sposob-1-prinos-sloev-i-staticheskih-resursov-v-volume,-montiruemyj-k-polьzovatelьskomu-boksu-kak-read-only).

## Установка секьюрных прав на статические ресурсы.
Для того, чтобы секреты, приносимые в файлы статическим ресурсом, были невидны пользователю nobody, на данный статический ресурс можно установить права доступа.

Возможные варианты прав доступа:

`unmodifed` - Если ресурс закачивается по url, то подовый агент не меняет права доступа к ресурсу. Во всех остальных случаях файл с ресурсом создается с правами по умолчанию - 664, т.е. для user_id loadbase - чтение и запись, для group_id loadbase - чтение и запись, для всех остальных - только чтение.

`660` - На файлы ресурса выставляются права: для user_id loadbase - чтение и запись, для group_id loadbase - чтение и запись, для всех остальных - никаких прав.

`600` - На файлы ресурса выставляются права: для user_id loadbase - чтение и запись, для group_id loadbase - никаких прав, для всех остальных - никаких прав.

**Установка прав через спеку c использованием dctl:**

{% cut "Пример спецификации" %}
```yaml
......
static_resources:
- files:
    files:
    - file_name: yp_token
      secret_data:
        id: yp-token
        alias: '....:....'
  id: tokens
  access_permissions: '660'
  verification:
    check_period_ms: 60000
    checksum: 'EMPTY:'
......    
```
{% endcut %}

**Установка прав через UI:** 
![image](https://jing.yandex-team.ru/files/amich/secret_perm.png).

{% note alert %}

Нельзя в одном статическом ресурсе использовать секреты и обычные файлы, для секретов должны быть созданы отдельные статические ресурсы.

{% endnote %} 

Пример полной спеки с установкой прав доступа на статический ресурс tokens [тут](sox-service#sposob-1-prinos-sloev-i-staticheskih-resursov-v-volume,-montiruemyj-k-polьzovatelьskomu-boksu-kak-read-only).

## Read only rootfs для контейнеров боксов.
В sox сервисах основные бинарные файлы, приносимые слоями, и конфиги, приносимые статическими ресурсами, должны быть read only. Для решения данной задачи на стороне deploy реализована возможность запускать контейнеры боксов с read only rootfs. Для того, чтобы сделать необходимые папки на readonly rootfs как writable, необходимо примонтировать writable неперсистентный volume в данную папку.

**Развертываение пользовательского бокса с readonly rootfs через dctl:**

{% cut "Пример спецификации" %}

```yaml
...
boxes:
- id: base_box
  rootfs:
    create_mode: 'read_only'
...
```
{% endcut %}

**Монтирование writable volume в папку /var/log через dctl:**

{% cut "Пример спецификации" %}

```yaml
...
volumes:
- id: writable_volume
  generic: {}
  persistence_type: non_persistent
...
boxes:
- id: "base_box"
  volumes:
    - mount_point: /var/log
      volume_ref: writable_volume
      mode: 'read_write'
```
{% endcut %}

**Развертывание пользовательского бокса с read only rootfs через UI:**
![image](https://jing.yandex-team.ru/files/dkochetov/read_only_2.png)


**Монтирование writable volume в папку /var/log через UI:**
Добавляется вольюм в настройках деплой юнита во вкладке Disks, volumes and resources.
![image](https://jing.yandex-team.ru/files/dkochetov/writable_volume.png)

В настройках бокса во вкладке Resources вольюм монтируется к папке /var/logs.
![image](https://jing.yandex-team.ru/files/dkochetov/vol_2.png)

Пример полной спеки с приносом read only rootfs для base_box [тут](https://wiki.yandex-team.ru/users/dkochetov/securityfeaturesdoc/#6.1primerspekisreadonlyboxrootfsrezhimomchild-onlydljaboksasecretenvdljaperemennyxssekretamiipravamidostupanafajjlyssekretami).


{% cut "Пример работы" %}
```bash
dkochetov@sas1-8015:~$ sudo portoctl shell ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box
(ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box)root@pyqspjxmzks3gugc:/# echo 1111 > file.txt 
bash: file.txt: Read-only file system
(ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box)root@pyqspjxmzks3gugc:/# echo 1111 > /var/log/file.txt 
(ISS-AGENT--pyqspjxmzks3gugc/pod_agent_box_base_box)root@pyqspjxmzks3gugc:/# ls -la /var/log/file.txt 
-rw-rw-r-- 1 root root 5 Sep 27 09:02 /var/log/file.txt
```
{% endcut %}

Из вышеописанного примера видим, что box rootfs является read only, кроме папки /var/log, так как мы примонтировали в нее writable volume

**Особенности**
1. На текущий момент у порто имеется ограничение: невозможно примонтировать вольюм к read only rootfs к несуществующей папке. Рассмотрим следующий кейс. Сервису необходима папка в rootfs /app/logs как writable и изначально данной папки нету в слоях, из которых собирается rootfs. Нам нужно принести данную папку отдельным лейром в рутфс:

{% cut "Пример" %}

    ```bash
    mkdir -p app/logs
    tar -czvf app
    tar -czvf app app_logs_layer.tar.gz
    ya upload app_logs_layer.tar.gz --ttl=inf
    Created resource id is 2462862388
	    TTL          : INF
	    Resource link: https://sandbox.yandex-team.ru/resource/2462862388/view
	    Download link: https://proxy.sandbox.yandex-team.ru/2462862388
    ```
    в спеке:
    ```yaml
    resources:
      layers:
      ...
      - checksum: "EMPTY:"
        id: app_logs_layer
        url: "https://proxy.sandbox.yandex-team.ru/2462862388"

    boxes:
    - id: "base_box"
      rootfs:
        create_mode: "read_only"
        layer_refs:
        ....
        - app_logs_layer
    ```
    Теперь к данной папке можно монтировать writable неперсистентный вольюм и она станет как writable на read only rootfs.

{% endcut %}

2. Начиная с версии runtime_revision 7 в случае использования read only rootfs бокса спека пользователя автоматом дообогощается слоями с системными папками и необходимыми вольюмами для writable папок для deploy sidecars: pod_agent, logbroker, coredump, logrotate, dru, juggler. Подробности [тут](https://st.yandex-team.ru/DEPLOY-4870).


## Возможность приносить слои и статические ресурсы в volume, монтируемый к боксу как read only.
В случае, если сокс сервису для работы требуется много writable папок, и если некритично, где будут располагаться read only файлы(бинарные файлы и статические ресурсы), то намного проще приносить эти файлы в volume, монтируемый к box rootfs как read only, нежели делать весь бокс rootfs как read only.

**Принос лейров и статических ресурсов в volume, монтируемый к боксу как read only через dctl:**

{% cut "Пример спецификации" %}


```yaml
.....
volumes:
- id: readonly_volume
  generic:
    layer_refs:
    - simple_http_server
  static_resources:
  - resource_ref: 'configs'
    volume_relative_mount_point: /configs
.....
.....
boxes:
- id: base_box
  volumes:
  - mount_point: /app/bin
      volume_ref: readonly_volume
      mode: 'read_only'
....
```
{% endcut %}

**Принос лейров и статических ресурсов в volume, монтируемый к боксу как read only через UI:**
Добавляется вольюм в настройках деплой юнита во вкладке Disks, volumes and resources.
![image](https://jing.yandex-team.ru/files/dkochetov/screenshot_3-1.png)

В настройках бокса во вкладке Resources вольюм монтируется к папке /app/bin.
![image](https://jing.yandex-team.ru/files/dkochetov/screenshot_2-1.png)

{% cut "Пример работы" %}

```bash
dkochetov@sas2-6806:~$ sudo portoctl shell ISS-AGENT--kckpkmif7lrmb6qc/pod_agent_box_base_box

(ISS-AGENT--kckpkmif7lrmb6qc/pod_agent_box_base_box)root@kckpkmif7lrmb6qc:/app/bin# ls
configs  simple_http_server
(ISS-AGENT--kckpkmif7lrmb6qc/pod_agent_box_base_box)root@kckpkmif7lrmb6qc:/app/bin# echo 111 >> simple_http_server 
bash: simple_http_server: Read-only file system
(ISS-AGENT--kckpkmif7lrmb6qc/pod_agent_box_base_box)root@kckpkmif7lrmb6qc:/app/bin# echo 111 >> configs/config 
bash: configs/config: Read-only file system
(ISS-AGENT--kckpkmif7lrmb6qc/pod_agent_box_base_box)root@kckpkmif7lrmb6qc:/app/bin# cd ../..
(ISS-AGENT--mjteiyjsx5e44jx2/pod_agent_box_base_box)root@kckpkmif7lrmb6qc:/# echo 1111 > file.txt 
(ISS-AGENT--mjteiyjsx5e44jx2/pod_agent_box_base_box)root@kckpkmif7lrmb6qc:/# ls -la file.txt 
-rw-rw-r-- 1 root root 5 Sep 27 10:33 file.txt
```
{% endcut %}

Из примера выше видим, что rootfs бокса writable, кроме папки /app/bin, в которую мы примонтировали volume как read only.
В папке /app/bin находятся бинарный файл из слоя simple_http_server и файлы из статического ресурса configs.

Пример полной спеки с приносом слоев в volume, монтируемым к rootfs пользовательского base_box как read only [тут](sox-service#sposob-1-prinos-sloev-i-staticheskih-resursov-v-volume,-montiruemyj-k-polьzovatelьskomu-boksu-kak-read-only).


**Особенности**
Со стороны подового агента запрещается приносить один и тот же статический ресурс в вольюм, который монтируется к боксу как read only и в бокс с writable rootfs.
Со стороны подового агента запрещается приносить один и тот же статический ресурс в вольюм, который монтируется к боксу как read only и в volume, который монтируется к боксу как read write.
