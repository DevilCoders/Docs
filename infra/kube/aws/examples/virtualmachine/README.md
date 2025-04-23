# VirtualMachine

In this example we'll deploy VirtualMachine in AWS

## Prerequisites

* Set up kubernetes environment with crossplane

  You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

* You need [nets](../net) provisioned

## Provision

1. Read your public ssh key data to add it on instance

```shell
export KEY_DATA=$(cat ~/.ssh/id_rsa.pub)
```

2. Create Instance resources

```shell
cat infra/kube/aws/examples/virtualmachine/*.yaml | envsubst | kubectl --context crossplane apply -f -
```

3. Watch resources status

```shell
watch kubectl --context crossplane get -f infra/kube/aws/examples/virtualmachine/
```

## Check Instance

// TODO: add how to ssh connect vm guide

## Find resource in UI

// TODO: add guide
