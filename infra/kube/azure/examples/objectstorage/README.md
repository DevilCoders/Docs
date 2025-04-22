# Object storage

In this example we'll provision Storage Account in Azure

## Prerequisites

* Set up kubernetes environment with crossplane

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision

1. Provision `samplekubestorage` storage account

```shell
kubectl --context yc-crossplane apply -f infra/kube/azure/examples/objectstorage
```

2. Check statuses

```shell
kubectl --context yc-crossplane get -f infra/kube/azure/examples/objectstorage
```

## Further read

* [Guides from Azure for different languages how to work with Storage Account](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)
* [Microsoft docs about Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)
