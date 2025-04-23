# Getting started with Crossplane over AWS

In this guide we'll:

* Setup tools to work with AWS
* Get access to interact with AWS

## About system

* We have communal kubernetes cluster with installed controllers to deploy and manage Azure resources (Later "Crossplane
  cluster"). Example resources: managed kubernetes cluster to deploy application, managed databases to use with
  application.

* To deploy our application we'll use another kubernetes cluster(s) in AWS. (Later EKS)

* Both clusters controlling with single tool kubectl with
  multiple [contexts](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-context-and-configuration).

## Prerequisites

In this guide we'll use cli tools:

* kubectl - main tool to work with kubernetes
* yc CLI - CLI for Yandex.Cloud

Also we need roles on Azure resources.

[Guide](prerequisites.md), how to request access and setup tools.

## Explore other examples

More examples about infrastructure provisioning can be found in [infra/kube/azure/examples](../examples).
