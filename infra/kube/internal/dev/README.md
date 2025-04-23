# Описание окружений

## Production

Link: https://console.cloud.yandex.ru/folders/b1gjmmtufqjb87p5tojj?section=dashboard

Конфигурация YC:

```
yc init --folder-id b1gjmmtufqjb87p5tojj --cloud-id b1gjk8shtb2smi1cgqdn --federation-id yc.yandex-team.federation
```

```
yc managed-kubernetes cluster get-credentials --id catto5c16ffeqd1fqinl --external

```

## Preprod

Link: https://console.cloud.yandex.ru/folders/b1gl3b8gmea01lcfpifp?section=dashboard

Конфигурация YC:

```
yc init --folder-id b1gl3b8gmea01lcfpifp --cloud-id b1gjk8shtb2smi1cgqdn --federation-id yc.yandex-team.federation
```

Подключиться к кластеру k8s:

```
yc managed-kubernetes cluster get-credentials --id catarj79iq0h0i31d10j --external

```

----

Описания ролей доступны в bb:

https://bb.yandex-team.ru/projects/CROSSPLANE/repos/provider-yc/browse/examples/roles
