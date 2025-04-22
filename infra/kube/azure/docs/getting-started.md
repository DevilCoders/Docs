# Getting started guide with Azure

In this guide we'll:

* Setup tools to work with Azure
* Get access to interact with Azure
* Learn how to provision Azure managed services
* Learn how to deploy application

## About system

* We have communal kubernetes cluster with installed controllers to deploy and manage Azure resources (Later "Crossplane
  cluster"). Example resources: managed kubernetes cluster to deploy application, managed databases to use with
  application.

* To deploy our application we'll use another kubernetes cluster(s) in Azure. (Later AKS)

* Both clusters controlling with single tool kubectl with
  multiple [contexts](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-context-and-configuration).

## Prerequisites

In this guide we'll use cli tools:

* kubectl - main tool to work with kubernetes
* yc CLI - CLI for Yandex.Cloud
* az CLI - CLI for Azure

Also we need roles on Azure resources.

[Guide](prerequisites.md), how to request access and setup tools.

## Bootstrap AKS from Crossplane cluster

Look in example configurations in [infra/kube/azure/examples/kubernetes](../examples/kubernetes). Changed needed
options. Full list of configuration options can be found with `kubectl exaplain <resource kind>`

After simply apply full set of resources in Crossplane cluster:

```shell
kubectl --context yc-crossplane apply -f infra/kube/azure/examples/kubernetes
```

Wait for all resources becomes READY:

```shell
watch kubectl --context yc-crossplane get -f infra/kube/azure/examples/kubernetes
```

Setup kubectl context for AKS. Instruction can be found in [prerequisites.md](prerequisites.md) under kubectl section.

## Provision Docker registry

[Guide about how to setup registry.](../examples/registry)

## Provision postgresql cluster

Example configurations are in [infra/kube/azure/examples/postgresql](../examples/postgresql)

Like with kubernetes apply and wait resources ready:

```shell
kubectl --context yc-crossplane apply -f infra/kube/azure/examples/postgresql
watch kubectl --context yc-crossplane get -f infra/kube/azure/examples/postgresql
```

## Deploy demo application in AKS that works with PostgreSQL

How to deploy application works with postgresql [guide](../../examples/deployments/postgresql).

## Explore other examples

More examples about infrastructure provisioning can be found in [infra/kube/azure/examples](../examples).

Examples from ASO
authors: [github.com/Azure-Samples/azure-service-operator-samples](https://github.com/Azure-Samples/azure-service-operator-samples)
