# VirtualMachine

In this guide we'll provision VirtualMachine instance in Yandex Cloud.

## Prerequisites

* Set up kubernetes environment with crossplane
* Reconciled core resources

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision

1. Read your public ssh key data to add it on instance

```shell
export KEY_DATA=$(cat ~/.ssh/id_rsa.pub)
```

2. Fill `KEY_DATA` in `spec.forProvider.metadata.ssh-keys` and apply kubernetes resources

```shell
cat infra/kube/yc/examples/virtualmachine/*.yaml | envsubst | kubectl --context yc-crossplane apply -f -
```

3. Check resources statuses. Wait then both SYNCED and READY becomes True:

```shell
kubectl --context yc-crossplane get -f infra/kube/yc/examples/virtualmachine
```

4. Find public IP address in `status.atProvider.networkInterface.0.natIpAddress`:

// TODO: This one not working for now. You need go to UI cloud console to find IP addr.

```shell
kubectl --context yc-crossplane get -f infra/kube/yc/examples/virtualmachine -o yaml
```

5. Connect vm:

```shell
ssh <public-ip-addr>
```

## Further read

* [Yandex Cloud doc about Compute](https://cloud.yandex.com/en-ru/services/compute)
