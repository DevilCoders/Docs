# Getting started

In this guide we'll:

* Setup tools to work with Yandex Cloud
* Get access to interact with Yandex Cloud
* Learn how to provision Yandex Cloud managed services
* Learn how to deploy application Yandex Cloud managed kubernetes

Cloud console UI links:

* [PROD](https://console.cloud.yandex.ru/federations/yc.yandex-team.federation)
* [PREPROD](https://console-preprod.cloud.yandex.ru/federations/yc.yandex-team.federation)

## About system

* We have communal kubernetes cluster with installed controllers to deploy and manage Yandex Cloud resources (Later "
  Crossplane cluster"). Example resources: managed kubernetes cluster to deploy application, managed databases to use
  with application.

* To deploy our application we'll use another kubernetes cluster(s) in Yandex Cloud. (Later Mk8s)

* Both clusters controlling with single tool kubectl with
  multiple [contexts](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-context-and-configuration).

## Prerequisites

In this guide we'll use cli tools:

* kubectl - main tool to work with kubernetes
* yc CLI - CLI for Yandex.Cloud

Also we need roles on Yandex Cloud resources.

[Guide](prerequisites.md), how to request access and setup tools.

## Provision Mk8s from Crossplane cluster

[Guide about how to setup mk8s.](../examples/kubernetes)

## Provision Docker Registry

[Guide about how to setup registry.](../examples/registry)

## Provision PostgreSQL cluster

[Guide about how to setup PostgreSQL.](../examples/postgresql)

## Deploy demo application in Mk8s that works with PostgreSQL

How to deploy application works with postgresql [guide](../../examples/deployments/postgresql).

## Explore other examples

More examples about infrastructure provisioning can be found in [examples](../examples).
