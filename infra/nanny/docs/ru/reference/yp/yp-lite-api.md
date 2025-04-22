# API создания и удаления подов YP_LITE

##  Зачем? {#why}

YP_LITE представляет собой расширение модели сервиса Nanny, поддерживающее деплой поверх подов YP. Поскольку оно реализовано в Nanny, в нём существует ряд ограничений. Например, Nanny.YP_LITE создаёт поды с предзаполненными полями, без которых alemate в последствии не сможет выполнять деплой на них. Из-за этого прямое использование API YP для аллокации подов, поверх которых будет деплой в Nanny.YP_LITE затруднительно. Поэтому Nanny предоставляет проксирующее API поверх YP, использование которого возможно только для деплоя в YP_LITE (не совместимо c Яндекс.Друг).

##  Полезные ссылки {#links}

Адрес API
* [https://yp-lite-ui.nanny.yandex-team.ru/api/yplite/pod-sets/](https://yp-lite-ui.nanny.yandex-team.ru/api/yplite/pod-sets/)
* [https://yp-lite-ui.nanny.yandex-team.ru/api/yplite/endpoint-sets/](https://yp-lite-ui.nanny.yandex-team.ru/api/yplite/endpoint-sets/) 
* [https://yp-lite-ui.nanny.yandex-team.ru/api/yplite/pod-reallocation/](https://yp-lite-ui.nanny.yandex-team.ru/api/yplite/pod-reallocation/)

proto-файлы 
* [https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/yp_lite_api/proto](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/yp_lite_api/proto) содержат описание доступных методов и схемы запросов и ответов

##  Аутентификация {#authn}
Поддерживается по одному из способов:

1. OAuth-токену приложения Nanny API, который можно получить [тут](https://nanny.yandex-team.ru/ui/#/oauth/);
1. OAuth-токену со скоупом `nanny:all`;
1. `Cookie: session_id`.

##  Авторизация {#authorization}
YP_LITE проверяет права пользователя (аутентифицированного по токену или сессии) на Nanny-сервис. Если пользователь может изменять Nanny-сервис, то и YP-объекты, связанные с этим сервисом доступны на запись (и чтение) через YP_LITE, иначе YP_LITE позволяет только читать YP-объекты.

##  Связь YP-объектов с Nanny-сервисами {#pod-set-service-relation}
* Nanny-сервисы (тонее говоря, YP_LITE-сервисы) и подсеты YP связаны друг с другом отношением 1:1, `pod_set_id = service_id.replace('_', '-')`
* При создании подов и подсетов через `YP_LITE` в лейбле `nanny_service_id` прописывается id соответствующего Nanny-сервиса

##  Особенности работы с YP-lite API {#caveats}
При работе с YP-lite API нужно учитывать следующие **критические особенности**:

1. При удалении сервиса, в котором ранее были созданы поды, необходимо всегда первым действием сначала удалять поды, и только затем сервис. В противном случае поды этого сервиса останутся занимать квоту навечно (пока не придёт человек и не удалит их явно).
1. Для идемпотентной обработки операций нужно использовать заголовок `X-Req-Id`. Это критично, например, при создании подов: если первый запрос был обработан, но клиент не получил ответ и поретраил его, чтобы избежать повторного создания подов, нужно выставлять одинаковый заголовок `X-Req-Id` в обоих запросах. При этом первый запрос получит ответ 200, второй 409.

##  Клиент для python {#python-client}
Сделан на базе `nanny_rpc_client`. Для общения с сервером сериализует запросы/десериализует ответы в protobuf, что эффективнее использования json.
Пример использования клиента: [https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/yp_lite_api/py_example/__main__.py](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/yp_lite_api/py_example/__main__.py)

##  Пример с json {#example-json}
```json
i024@i024-nix:~$ cat ~/y/CreatePodSet.json
{
"allocationRequest": {
  "annotations": [],
  "anonymousMemoryLimitMegabytes": 0,
  "enableInternet": false,
  "hostDevices": {
    "devKvm": "Disable"
    },
  "labels": [],
  "memoryGuaranteeMegabytes": 512,
  "memoryLimitMegabytes": 512,
  "networkMacro": "_GENCFG_SEARCHPRODNETS_ROOT_",
  "persistentVolumes": [
    {
      "diskQuotaMegabytes": 5120,
      "mountPoint": "/logs",
      "storageClass": "hdd"
    }
  ],
  "replicas": 1,
  "rootFsQuotaGigabytes": 0,
  "rootFsQuotaMegabytes": 1024,
  "rootVolumeStorageClass": "hdd",
  "snapshotsCount": 10,
  "sysctlProperties": [],
  "vcpuGuarantee": 1000,
  "vcpuLimit": 1000,
  "virtualServiceIds": [],
  "workDirQuotaGigabytes": 0,
  "workDirQuotaMegabytes": 1024
  },

"antiaffinityConstraints": {
  "nodeMaxPods": 1,
  "rackMaxPods": 0
  },

"cluster": "SAS",

"quotaSettings": {
  "abcServiceId": 664,
  "mode": "ABC_SERVICE"
  },

"serviceId": "saas_yp_cloud_saas_knn_prestable"
}
i024@i024-nix:~$ curl -H "Authorization: OAuth $OAUTH_NANNY" -H "Content-Type: text/plain" -X POST -d @y/CreatePodSet.json 'https://yp-lite-ui.nanny.yandex-team.ru/api/yplite/pod-sets/CreatePodSet/'
{"podIds":["qaakco33hs6ajo7q"],"podSetId":"saas-yp-cloud-saas-knn-prestable"}
```
