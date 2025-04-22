## IAM User

In this example we'll create IAM user for LoadBalancer

## Prerequisites

* Set up kubernetes environment with crossplane
* Set up aws cli locally

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision

Create IAM user, IAM Policy to read ec2, attach Policy to User

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/iamuser
```

Watch statuses:

```shell
watch kubectl --context crossplane get -f infra/kube/aws/examples/iamuser
```
