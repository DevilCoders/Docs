# Публичный API pod_agent

По умолчанию pod_agent слушает 1 порт и принимает http запросы:

## localhost:1/pod_attributes

```json
$: curl localhost:1/pod_attributes
{
  "node_meta": { // информация о ноде
    "dc": "sas",                             // DC в котором находится нода, может не соответствовать yp кластеру, ибо, например, на sas-test есть ноды из iva
    "cluster": "sas.yp.yandex.net",          // fqdn мастера yp, ибо кластер yp может не соответствовать DC, где находится нод
    "fqdn": "sas3-5396.search.yandex.net"    // fqdn ноды, на которой находится под
  },
  "resource_requirements": {  // ресурсы, выделенные на под
    "cpu": {
      "cpu_limit_millicores": 497.3076923,
      "cpu_guarantee_millicores": 497.3076923
    },
    "memory": {
      "memory_guarantee_bytes": 33554432,
      "memory_limit_bytes": 67108864
    }
  },
  "metadata": {  // атрибуты пода
    "annotations": {
      "<annot_key>": "<annot_value>"
    },
    "labels": {
      "<label_key>": "<label_value>"
    },
    "pod_id": "<yp_pod_id>",
  },
  "box_resource_requirements": {  // боксы из текущей target spec - множество активных на данный момент боксов может быть другим
    "<box_id>": {
      "cpu": {
        "cpu_limit_millicores": 397.8461538,
        "cpu_guarantee_millicores": 397.8461538
      },
      "memory": {
        "memory_guarantee_bytes": 33554432,
        "memory_limit_bytes": 67108864
      }
    }
  },
  // Json представление вот этого protobuf message: https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/data_model.proto?rev=7147587#L1507-1547
  "ip6_address_allocations": [
    {
      "internet_address": {
        "ip4_address": "ip4_test",
        "id": "test_id"
      },
      "transient_fqdn": "man3-0442-1.man3-0442-node-hume.man-pre.yp-c.yandex.net",
      "persistent_fqdn": "man3-0442-node-hume.man-pre.yp-c.yandex.net",
      "virtual_services": [],
      "address": "2a02:6b8:c0a:1808:10d:2342:42d5:0",
      "vlan_id": "backbone",
      "labels": {
        "label_key": "label_value"
      }
    },
    {
      "transient_fqdn": "fb-man3-0442-1.man3-0442-node-hume.man-pre.yp-c.yandex.net",
      "persistent_fqdn": "fb-man3-0442-node-hume.man-pre.yp-c.yandex.net",
      "virtual_services": [],
      "address": "2a02:6b8:fc12:1808:10d:2342:b557:0",
      "vlan_id": "fastbone",
      "labels": {}
    }
  ]
  // Json представление вот этого protobuf message: https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/data_model.proto?rev=7147587#L1565-1611
  // Ждет релиза DEPLOY-2227
  "disk_volume_allocations": [
    {
      "id": "pod-agent-test-stage-on-sas-test-allocation",
      "labels": {},
      "capacity": 5368709120,
      "resource_id": "disk-place-sas2-6807-search-yandex-net",
      "volume_id": "824bf042-ca1ceb9f-4aaff001-ac035535",
      "device": "/place",
      "read_bandwidth_guarantee": 0,
      "read_bandwidth_limit": 0,
      "write_bandwidth_guarantee": 0,
      "write_bandwidth_limit": 0,
      "read_operation_rate_guarantee": 0,
      "read_operation_rate_limit": 0,
      "write_operation_rate_guarantee": 0,
      "write_operation_rate_limit": 0
    },
    {
      "id": "pod_agent",
      "labels": {
        "used_by_infra": true
      },
      "capacity": 1073741824,
      "resource_id": "disk-place-sas2-6807-search-yandex-net",
      "volume_id": "824bf043-8c3e41b-867308fc-1130aa43",
      "device": "/place",
      "read_bandwidth_guarantee": 0,
      "read_bandwidth_limit": 0,
      "write_bandwidth_guarantee": 0,
      "write_bandwidth_limit": 0,
      "read_operation_rate_guarantee": 0,
      "read_operation_rate_limit": 0,
      "write_operation_rate_guarantee": 0,
      "write_operation_rate_limit": 0
    }
  ],
}
```
