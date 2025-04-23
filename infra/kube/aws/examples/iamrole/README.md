## IAM Role

In this example we'll create IAM roles for Kubernetes

## Prerequisites

* Set up kubernetes environment with crossplane
* Set up aws cli locally

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision

Create IAM role, attach Policies to Role needed for EKS (Managed kubernetes):

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/iamrole
```

Watch statuses:

```shell
watch kubectl --context crossplane get -f infra/kube/aws/examples/iamrole
```
