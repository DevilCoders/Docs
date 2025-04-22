# Настраиваем kubectl на работу с crossplane в Yandex.Cloud

## Логинимся в ui yandex cloud

Заходим в Yandex Cloud через SSO: https://console.cloud.yandex.ru/federations/yc.yandex-team.federation

## Настраиваем yc

1. Устанавливаем yc, следуя официальной [инструкции](https://cloud.yandex.ru/docs/cli/operations/install-cli).
2. Иницализируем:

    ```shell
    yc init --federation-id=yc.yandex-team.federation --cloud-id=b1gjk8shtb2smi1cgqdn --folder-name=crossplane --profile=crossplane
    ```

* Утилита попросит открыть браузер и аутентифицироваться в нём. Нажимаем `Enter`.
* На вопрос `Do you want to configure a default Compute zone? [Y/n]` отвечаем `n`.

## Настраиваем kubectl для работы с k8s в Yandex.Cloud

Добавляем конфиг для работы с yc k8s.

```shell
yc managed-kubernetes cluster get-credentials --external --folder-name=crossplane --name=crossplane --context-name crossplane
```

## Проверяем успешность установки

```shell
❯ kubectl --context crossplane cluster-info
Kubernetes control plane is running at https://178.154.240.5
CoreDNS is running at https://178.154.240.5/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://178.154.240.5/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

❯ kubectl --context crossplane api-resources
NAME                                  SHORTNAMES     APIVERSION                                        NAMESPACED   KIND
bindings                                             v1                                                true         Binding
componentstatuses                     cs             v1                                                false        ComponentStatus
configmaps                            cm             v1                                                true         ConfigMap
---
```
