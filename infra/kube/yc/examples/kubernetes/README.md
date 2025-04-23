# Kubernetes

In this example we'll:

* Deploy Managed Kubernetes cluster
* Setup kubectl config for deployed cluster

## Prerequisites

* Set up kubernetes environment with crossplane
* Set up yc cli
* Reconciled core resources

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision

### Deploy kubernetes cluster

Due to compliance reasons we must use internal kubernetes endpoint. Be sure you have network connectivity with private
VPC via bastion or jump vm or etc.

1. Walk through resources specs and edit needed fields

* [Cluster](cluster.yaml)
* [NodeGroup](nodegroup.yaml)
* [KMS](kms.yaml)
* [ServiceAccount](serviceaccount.yaml)
* [ServiceAccount roles](serviceaccountroles.yaml)

2. Deploy kubernetes cluster with all needed dependencies.

```shell
kubectl --context yc-crossplane apply -f infra/kube/yc/examples/kubernetes
```

3. Check resources statuses. Wait then both SYNCED and READY becomes True:

```shell
kubectl --context yc-crossplane get -f infra/kube/yc/examples/kubernetes
```

### Setup kubectl config

1. List all clusters and find needed:

```shell
yc managed-kubernetes cluster list
```

2. Update kubectl config with new context:

```shell
yc managed-kubernetes cluster get-credentials --id <cluster-id> --internal
```

### Further read

* [Image of demo application](../../../examples/demo-images/static)
* [Deploy application](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/)
* [Yandex Cloud doc about Managed Kubernetes](https://cloud.yandex.com/en-ru/services/managed-kubernetes)
