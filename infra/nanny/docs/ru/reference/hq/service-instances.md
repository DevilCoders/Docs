# Получение инстансов сервиса

##  Через HQ: получение всех ревизий всех инстансов сервиса с текущими состояниями {#hq}
HQ имеет отдельные не связанные между собой инсталляции в каждой из географических локаций: отдельная инсталляция в MAN, отдельная в SAS, VLA и MSK.
Инстансы сервиса можно получить, сделав запрос в каждую из требуемых локацией HQ. При закрытии по сети кластера с данной инсталляцией, она и только она, очевидно, будет недоступна.
Описано в [документации по HQ](https://wiki.yandex-team.ru/runtime-cloud/nanny/hq/api/).

##  Через Nanny: инстансы конкретного снэпшота {#nanny-snapshot-instances}
Инстансы конкретной ревизии сервиса можно получить через проксирующий запрос в Nanny. API-сервер Nanny выполнит проксирующие запросы в локационные инсталляции ISS и HQ и объединит их ответ. Существуют два различных метода в этом семействе:

1. Возвращающий "или полный ответ по всем инстансам, или ничего (502)";
1. Возвращающий инстансы из доступных локаций и список локаций, выполнить запрос в которые не удалось.

####  Полный список инстансов снэпшота {#nanny-snapshot-instances}
**Внимание** Данный метод API не работает при недоступности хотя бы одного кластера, т.е. отдаётся или полный ответ, или метод не отвечает (отдаёт 502).

* Шаблон запроса: `/v2/services/instances/<_id>/sn/<snapshot_id>/[?limit=<int>&skip=<int>]`
* Пример: `/v2/services/instances/admin_nanny/sn/3931c044d4157ed51a8adb04dfbe7723154c1c02/`

Пример ответа:
```json
{
    "instances": [
        {
            "configuration_family": "admin_nanny",
            "configuration_id": "admin_nanny#admin_nanny-1549366120347",
            "configuration_name": "admin_nanny-1549366120347",
            "current_state": "ACTIVE",
            "engine": "ISS_MAN",
            "host": "man1-8080.search.yandex.net",
            "host_short": "man1-8080",
            "hostname": "man1-8080.search.yandex.net",
            "hq_cluster": "man_prod",
            "hq_id": "man1-8080.search.yandex.net:8000@admin_nanny",
            "hq_rev": "admin_nanny-1549366120347",
            "instance_id": "admin_nanny#admin_nanny-1549366120347/8000@man1-8080.search.yandex.net",
            "properties": {},
            "service": "8000",
            "slot": "8000@man1-8080.search.yandex.net",
            "slot_short": "8000",
            "tags": {
                "ctype": "prod",
                "dc": "man",
                "geo": "man",
                "itype": "nanny",
                "prj": "admin-nanny"
            },
            "target_state": "ACTIVE"
        },
        {
            "configuration_family": "admin_nanny",
            "configuration_id": "admin_nanny#admin_nanny-1549366120347",
            "configuration_name": "admin_nanny-1549366120347",
            "current_state": "ACTIVE",
            "engine": "ISS_SAS",
            "host": "sas1-3793.search.yandex.net",
            "host_short": "sas1-3793",
            "hostname": "sas1-3793.search.yandex.net",
            "hq_cluster": "sas_prod",
            "hq_id": "sas1-3793.search.yandex.net:8000@admin_nanny",
            "hq_rev": "admin_nanny-1549366120347",
            "instance_id": "admin_nanny#admin_nanny-1549366120347/8000@sas1-3793.search.yandex.net",
            "properties": {},
            "service": "8000",
            "slot": "8000@sas1-3793.search.yandex.net",
            "slot_short": "8000",
            "tags": {
                "ctype": "prod",
                "dc": "sas",
                "geo": "sas",
                "itype": "nanny",
                "prj": "admin-nanny"
            },
            "target_state": "ACTIVE"
        },
        {
            "configuration_family": "admin_nanny",
            "configuration_id": "admin_nanny#admin_nanny-1549366120347",
            "configuration_name": "admin_nanny-1549366120347",
            "current_state": "ACTIVE",
            "engine": "ISS_VLA",
            "host": "vla1-4660.search.yandex.net",
            "host_short": "vla1-4660",
            "hostname": "vla1-4660.search.yandex.net",
            "hq_cluster": "vla_prod",
            "hq_id": "vla1-4660.search.yandex.net:8000@admin_nanny",
            "hq_rev": "admin_nanny-1549366120347",
            "instance_id": "admin_nanny#admin_nanny-1549366120347/8000@vla1-4660.search.yandex.net",
            "properties": {},
            "service": "8000",
            "slot": "8000@vla1-4660.search.yandex.net",
            "slot_short": "8000",
            "tags": {
                "ctype": "prod",
                "dc": "vla",
                "geo": "vla",
                "itype": "nanny",
                "prj": "admin-nanny"
            },
            "target_state": "ACTIVE"
        }
    ]
}
```

### Неполный список инстансов снэпшота

* Шаблон запроса: `/v2/services/instances/<_id>/sn/<snapshot_id>/partial/[?limit=<int>&skip=<int>]`
* Пример: `/v2/services/instances/admin_nanny/sn/3931c044d4157ed51a8adb04dfbe7723154c1c02/partial/`

Пример ответа:
```json
{
    "errors": [
        {
            "engine": "ISS_MSK",
            "error": "error: connection timeout 0.1s"
        }
    ],
    "instancesPart": [
        {
            "configuration_family": "admin_nanny",
            "configuration_id": "admin_nanny#admin_nanny-1549366120347",
            "configuration_name": "admin_nanny-1549366120347",
            "current_state": "ACTIVE",
            "engine": "ISS_MAN",
            "host": "man1-8080.search.yandex.net",
            "host_short": "man1-8080",
            "hostname": "man1-8080.search.yandex.net",
            "hq_cluster": "man_prod",
            "hq_id": "man1-8080.search.yandex.net:8000@admin_nanny",
            "hq_rev": "admin_nanny-1549366120347",
            "instance_id": "admin_nanny#admin_nanny-1549366120347/8000@man1-8080.search.yandex.net",
            "properties": {},
            "service": "8000",
            "slot": "8000@man1-8080.search.yandex.net",
            "slot_short": "8000",
            "tags": {
                "ctype": "prod",
                "dc": "man",
                "geo": "man",
                "itype": "nanny",
                "prj": "admin-nanny"
            },
            "target_state": "ACTIVE"
        },
        {
            "configuration_family": "admin_nanny",
            "configuration_id": "admin_nanny#admin_nanny-1549366120347",
            "configuration_name": "admin_nanny-1549366120347",
            "current_state": "ACTIVE",
            "engine": "ISS_SAS",
            "host": "sas1-3793.search.yandex.net",
            "host_short": "sas1-3793",
            "hostname": "sas1-3793.search.yandex.net",
            "hq_cluster": "sas_prod",
            "hq_id": "sas1-3793.search.yandex.net:8000@admin_nanny",
            "hq_rev": "admin_nanny-1549366120347",
            "instance_id": "admin_nanny#admin_nanny-1549366120347/8000@sas1-3793.search.yandex.net",
            "properties": {},
            "service": "8000",
            "slot": "8000@sas1-3793.search.yandex.net",
            "slot_short": "8000",
            "tags": {
                "ctype": "prod",
                "dc": "sas",
                "geo": "sas",
                "itype": "nanny",
                "prj": "admin-nanny"
            },
            "target_state": "ACTIVE"
        },
        {
            "configuration_family": "admin_nanny",
            "configuration_id": "admin_nanny#admin_nanny-1549366120347",
            "configuration_name": "admin_nanny-1549366120347",
            "current_state": "ACTIVE",
            "engine": "ISS_VLA",
            "host": "vla1-4660.search.yandex.net",
            "host_short": "vla1-4660",
            "hostname": "vla1-4660.search.yandex.net",
            "hq_cluster": "vla_prod",
            "hq_id": "vla1-4660.search.yandex.net:8000@admin_nanny",
            "hq_rev": "admin_nanny-1549366120347",
            "instance_id": "admin_nanny#admin_nanny-1549366120347/8000@vla1-4660.search.yandex.net",
            "properties": {},
            "service": "8000",
            "slot": "8000@vla1-4660.search.yandex.net",
            "slot_short": "8000",
            "tags": {
                "ctype": "prod",
                "dc": "vla",
                "geo": "vla",
                "itype": "nanny",
                "prj": "admin-nanny"
            },
            "target_state": "ACTIVE"
        }
    ]
}

```

### Через Nanny: инстансы последней целиком активированной ревизии

Данный метод опирается на эвристику выбора одной конкретной активной ревизии сервиса:
1. В случае, если сервис находится в стабильном состоянии, т.е. выкладок не запущено и есть активный снэпшот, то возвращаются его инстансы;
2. Если же сервис находится в процессе выкладки, то возвращается последний до конца успешно активированный снэпшот;
3. Если такого снэпшота нет, **или он уже удалён**, то возвращается снэпшот в статусе `ACTIVATING`; 4. Если же и такого нет, то перебираются статусы `ACTIVATION_MUST_BE_CANCELLED`, `DEACTIVATE_PENDING`, `BROKEN`.
При этом для получения инстансов API-сервер Nanny выполнит проксирующие запросы в локационные инсталляции ISS и HQ и объединит их ответ. Существуют два различных метода в этом семействе:
    1. Возвращающий "или полный ответ по всем инстансам, или ничего (502)";
    1. Возвращающий инстансы из доступных локаций и список локаций, выполнить запрос в которые не удалось.

####  Полный список инстансов {#nanny-current-instances}
**Внимание** Данный метод API не работает при недоступности хотя бы одного кластера, т.е. отдаётся или полный ответ, или метод не отвечает (отдаёт 502).

* Шаблон запроса: `/v2/services/<_id>/current_state/instances/`
* Пример: `/v2/services/production_setrace_msk/current_state/instances/`

Пример ответа:

```json
{
    "result": [
        {
            "container_hostname": "bb-sas1-2956-SAS_SETRACE_PRODU_B8F-27660.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "sas1-2956.search.yandex.net",
            "itags": [
                ...
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 27660
        },
        {
            "container_hostname": "bb-sas1-8490-SAS_SETRACE_PRODU_B8F-27660.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "sas1-8490.search.yandex.net",
            "itags": [
                ...
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 27660
        },
        {
            "container_hostname": "bb-sas1-6533-SAS_SETRACE_PRODU_B8F-27660.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "sas1-6533.search.yandex.net",
            "itags": [
                ...
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 27660
        },
        {
            "container_hostname": "bb-sas1-9217-SAS_SETRACE_PRODU_B8F-27660.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "sas1-9217.search.yandex.net",
            "itags": [
                ...
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 27660
        },
        {
            "container_hostname": "bb-sas1-2794-SAS_SETRACE_PRODU_B8F-27660.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "sas1-2794.search.yandex.net",
            "itags": [
                ...
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 27660
        }
    ]
}
```


####  Неполный список инстансов {#nanny-current-instances-partial}
* Шаблон запроса: `/v2/services/<_id>/current_state/instances/partial/`
* Пример: `/v2/services/production_setrace_msk/current_state/instances/partial/`

Пример ответа

```json
{
    "errors": [
        {
            "error": "error: connection timeout 0.1s",
            "location": "msk"
        }
    ],
    "instancesPart": [
        {
            "container_hostname": "man1-8080-man-admin-nanny-8000.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "man1-8080.search.yandex.net",
            "itags": [
                "MAN_ADMIN_NANNY",
                "a_ctype_prod",
                "a_dc_man",
                "a_geo_man",
                "a_itype_nanny",
                "a_line_man2",
                "a_metaprj_internal",
                "a_prj_admin-nanny",
                "a_tier_none",
                "a_topology_cgset-memory.limit_in_bytes=110595407872",
                "a_topology_cgset-memory.low_limit_in_bytes=3221225472",
                "a_topology_group-MAN_ADMIN_NANNY",
                "a_topology_stable-125-r1264",
                "a_topology_version-stable-125-r1264",
                "cgset_memory_recharge_on_pgfault_1",
                "enable_hq_report",
                "enable_hq_poll"
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 8000
        },
        {
            "container_hostname": "sas1-3793-sas-admin-nanny-8000.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "sas1-3793.search.yandex.net",
            "itags": [
                "SAS_ADMIN_NANNY",
                "a_ctype_prod",
                "a_dc_sas",
                "a_geo_sas",
                "a_itype_nanny",
                "a_line_sas-1.3.3",
                "a_metaprj_internal",
                "a_prj_admin-nanny",
                "a_tier_none",
                "a_topology_cgset-memory.limit_in_bytes=110595407872",
                "a_topology_cgset-memory.low_limit_in_bytes=3221225472",
                "a_topology_group-SAS_ADMIN_NANNY",
                "a_topology_stable-125-r1264",
                "a_topology_version-stable-125-r1264",
                "cgset_memory_recharge_on_pgfault_1",
                "enable_hq_report",
                "enable_hq_poll"
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 8000
        },
        {
            "container_hostname": "vla1-4660-vla-admin-nanny-8000.gencfg-c.yandex.net",
            "engine": "",
            "hostname": "vla1-4660.search.yandex.net",
            "itags": [
                "VLA_ADMIN_NANNY",
                "a_ctype_prod",
                "a_dc_vla",
                "a_geo_vla",
                "a_itype_nanny",
                "a_line_vla-01",
                "a_metaprj_internal",
                "a_prj_admin-nanny",
                "a_tier_none",
                "a_topology_cgset-memory.limit_in_bytes=110595407872",
                "a_topology_cgset-memory.low_limit_in_bytes=3221225472",
                "a_topology_group-VLA_ADMIN_NANNY",
                "a_topology_stable-125-r1264",
                "a_topology_version-stable-125-r1264",
                "cgset_memory_recharge_on_pgfault_1",
                "enable_hq_report",
                "enable_hq_poll"
            ],
            "network_settings": "NO_NETWORK_ISOLATION",
            "port": 8000
        }
    ]
}
```


####  Хосты последней целиком активированной ревизии {#current-hosts}
**Внимание** Данный метод API не работает при недоступности хотя бы одного кластера, т.е. отдаётся или полный ответ, или метод не отвечает (отдаёт 502).

* Шаблон запроса: `/v2/services/<_id>/current_state/hosts/`
* Пример: `/v2/services/production_setrace_msk/current_state/hosts/`

Пример ответа:

```json
{
    "result": [
        {
            "hostname": "ws37-384.yandex.ru"
        },
        {
            "hostname": "ws25-177.yandex.ru"
        },
        {
            "hostname": "mnews3-11.yandex.ru"
        },
        {
            "hostname": "ws38-381.yandex.ru"
        },
        {
            "hostname": "ws6-137.yandex.ru"
        }
    ]
}
```

Аналогичный метод с поддержкой неполного ответа:

* Шаблон запроса: `/v2/services/<_id>/current_state/hosts/partial/`
* Пример: `/v2/services/production_setrace_msk/current_state/hosts/partial/`

Пример ответа:

```json
{
    "errors": [
        {
            "error": "error: connection timeout 0.1s",
            "location": "msk"
        }
    ],
    "hostsPart": [
        {
            "hostname": "sas1-3793.search.yandex.net"
        },
        {
            "hostname": "man1-8080.search.yandex.net"
        },
        {
            "hostname": "vla1-4660.search.yandex.net"
        }
    ]
}
```
