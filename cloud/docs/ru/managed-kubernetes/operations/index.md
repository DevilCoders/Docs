---
title: Инструкции по работе с {{ managed-k8s-full-name }}
description: "Из статьи вы узнаете, как работать с управляемым сервисом {{ k8s }} в {{ yandex-cloud }}. Рассказываем, как работать с постоянными томами, управлять группой узлов и кластером {{ k8s }}."
---

# Все инструкции

* [{#T}](node-connect-ssh.md)
* [{#T}](update-kubernetes.md)
* [{#T}](autoscale.md)

## Подключение к кластеру {#cluster-connect}

* [{#T}](connect/index.md)
* [{#T}](connect/security-groups.md)
* [{#T}](connect/create-static-conf.md)

{% if product == "yandex-cloud" %}

## Установка приложений {#marketplace}

* [{#T}](applications/marketplace.md)
* [{#T}](applications/jaeger.md)
* [{#T}](applications/metrics-provider.md)

{% endif %}

## Сетевые сценарии {#network-scenarios}

* [{#T}](create-load-balancer.md)
* [{#T}](calico.md)
* [{#T}](cilium.md)
* [{#T}](cilium-node-local-dns.md)

## Работа с постоянными томами {#persistent-volumes}

* [{#T}](volumes/dynamic-create-pv.md)
* [{#T}](volumes/static-create-pv.md)
* [{#T}](volumes/manage-storage-class.md)
* [{#T}](volumes/volume-expansion.md)
* [{#T}](volumes/statefulset-pvc-expansion.md)
* [{#T}](volumes/mode-block.md)
* [{#T}](volumes/s3-csi-integration.md)

## Управление кластером {{ k8s }} {#kubernetes-cluster}

* [{#T}](kubernetes-cluster/kubernetes-cluster-list.md)
* [{#T}](kubernetes-cluster/kubernetes-cluster-create.md)
* [{#T}](kubernetes-cluster/kubernetes-cluster-update.md)
* [{#T}](kubernetes-cluster/kubernetes-cluster-namespace-create.md)
* [{#T}](kubernetes-cluster/kubernetes-cluster-delete.md)

## Управление группой узлов {#node-group}

* [{#T}](node-group/node-group-list.md)
* [{#T}](node-group/node-group-create.md)
* [{#T}](node-connect-ssh.md)
* [{#T}](autoscale.md)
* [{#T}](node-group/node-group-update.md)
* [{#T}](node-group/node-label-management.md)
* [{#T}](node-group/node-group-delete.md)

{% if product == "yandex-cloud" %}

## Работа с внешними узлами {#external-nodes}

* [{#T}](external-nodes-connect.md)

{% endif %}