# Intro
[Kubernetes API](https://kubernetes.io/docs/reference/using-api/api-concepts/) для доступа к K8s-объектам в системе InfraCtl.

Базовый URL: https://k.yandex-team.ru.

# Аутентификация
Аутентификация на данный момент только по OAuth-токену (по куке аутентификации нет). Для неаутентифицированных пользователей всегда возвращается код ответа 403 без редиректа на Паспорт.

Для аутентификации необходимо использовать OAuth-токен, добавив его в заголовки запросов: `Authorization: Bearer <access_token>`. Токен можно получить, пройдя по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=141d6d975f6049789ba7c78bf82ada5d) в браузере.

# Доступ через IDM
Пока что `https://k.yandex-team.ru` работает за WebAuth, поэтому необходимо запросить соответствующую роль в IDM по [ссылке](https://nda.ya.ru/t/axsT2X_h53EPbx).

# Схемы данных
Для описания схемы данных объектов, лежащих в K8s, используется protobuf.

* [DeployStage](https://a.yandex-team.ru/arc_vcs/infra/infractl/controllers/deploy/api/stage/proto_v1/deploystage_types.proto)
* [Runtime](https://a.yandex-team.ru/arc_vcs/infra/infractl/controllers/runtime/api/proto_v1/runtime_types.proto)

# Примеры работы с API через ванильный K8s-клиент на Python
Простейшие примеры создания и получения объекта типа DeployStage можно посмотреть по [ссылке](https://a.yandex-team.ru/arc_vcs/infra/infractl/samples/python/__main__.py).

# Пример создания объекта DeployStage напрямую через K8s API
```bash
reddi-lin:~$ cat ~/y/CreateDeployStage.json
{
  "apiVersion": "k.yandex-team.ru/v1",
  "kind": "DeployStage",
  "metadata": {
    "annotations": {
      "stage.infractl.k.yandex-team.ru/fqid": "yp|xdc|stage|infractl-api-demo|67259230-65b9d030-a805d396-3e830f75"
    },
    "name": "infractl-api-demo",
    "namespace": "infractl-demo-ns"
  },
  "spec": {
    "stage_spec": {
      "deploy_units": {
        "deployUnit": {
          "endpoint_sets": [
            {
              "port": 80
            }
          ],
          "network_defaults": {
            "network_id": "_SEARCHSAND_"
          },
          "replica_set": {
            "per_cluster_settings": {
              "sas": {
                "deployment_strategy": {
                  "max_unavailable": 1
                },
                "pod_count": 1
              }
            },
            "replica_set_template": {
              "constraints": {
                "antiaffinity_constraints": [
                  {
                    "key": "rack",
                    "max_pods": "1"
                  }
                ]
              },
              "pod_template_spec": {
                "spec": {
                  "disk_volume_requests": [
                    {
                      "id": "main-disk",
                      "labels": {
                        "attributes": [
                          {
                            "key": "used_by_infra",
                            "value": "BQ=="
                          }
                        ]
                      },
                      "quota_policy": {
                        "bandwidth_guarantee": "15728640",
                        "bandwidth_limit": "31457280",
                        "capacity": "3221225472"
                      },
                      "storage_class": "hdd"
                    }
                  ],
                  "host_infra": {
                    "monitoring": {
                      "labels": {
                        "itype": "infractl-demo-ns"
                      }
                    }
                  },
                  "pod_agent_payload": {
                    "spec": {
                      "boxes": [
                        {
                          "cgroup_fs_mount_mode": "ECgroupFsMountMode_RO",
                          "id": "box",
                          "rootfs": {
                            "layer_refs": [
                              "layer",
                              "simple_http_server"
                            ]
                          }
                        }
                      ],
                      "mutable_workloads": [
                        {
                          "workload_ref": "workload"
                        }
                      ],
                      "resources": {
                        "layers": [
                          {
                            "checksum": "EMPTY:",
                            "id": "layer",
                            "url": "sbr:2061235470"
                          },
                          {
                            "checksum": "EMPTY:",
                            "id": "simple_http_server",
                            "url": "sbr:755375039"
                          }
                        ]
                      },
                      "workloads": [
                        {
                          "box_ref": "box",
                          "id": "workload",
                          "readiness_check": {
                            "tcp_check": {
                              "port": 80
                            }
                          },
                          "start": {
                            "command_line": "/simple_http_server 80 'Hello my dear @reddi!'"
                          }
                        }
                      ]
                    }
                  },
                  "resource_requests": {
                    "memory_guarantee": "1073741824",
                    "memory_limit": "1073741824",
                    "network_bandwidth_guarantee": "10485760",
                    "vcpu_guarantee": "100",
                    "vcpu_limit": "100"
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}

reddi-lin:~$ curl -v -XPOST  -H "Authorization: Bearer XXX" -H "Accept: application/json" -H "Content-Type: application/json" 'https://k.yandex-team.ru/apis/k.yandex-team.ru/v1/namespaces/infractl-demo-ns/deploystages' -d @i/CreateDeployStage.json
```

