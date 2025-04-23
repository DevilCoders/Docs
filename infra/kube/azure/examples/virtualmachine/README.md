# VirtualMachine

In this example we'll deploy VirtualMachine in Azure

## Prerequisites

* Set up kubernetes environment with crossplane
* Set up az cli locally or use Cloud Shell in Azure Portal

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Resources we use

* [ResourceGroup](rg.yaml)
* [Virtual Networks](nets.yaml)

  Creating new virtual networks to place our vm.

* [Managed data disk](disk.yaml)

  Adding empty data disk to our vm.

* [PublicIPAddress](publicip.yaml)

  Creating public IP address to access our vm from outside private nets.

* [NetworkInterface](nic.yaml)
* [VirtualMachine](virtualmachine.yaml)

## Provision

```shell
export KEY_DATA=$(cat ~/.ssh/id_rsa.pub)
cat infra/kube/azure/examples/virtualmachine/*.yaml | envsubst | kubectl --context yc-crossplane apply -f -
```

## Resource in UI

1. Find resource id with:

```shell
kubectl --context yc-crossplane get virtualmachine.compute.azure.com/example-virtualmachine -o json | jq .status.id
```

2. Enter UI via link. Use last cmd output in `resource-id`:

```
"https://portal.azure.com/#@yandexteam.onmicrosoft.com/resource/<resource-id>"
```

## Self check

// TODO: add guide how to connect VM using only kubectl

**For now there is no way to get Public IP Address from ASO**

Press 'Connect' button on resource page in UI, follow instructions.
