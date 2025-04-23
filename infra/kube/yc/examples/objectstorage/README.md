# Object Storage example

In this example we'll provision Object Storage bucket with example object

## Prerequisites

* Set up kubernetes environment with crossplane
* Reconciled core resources

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision Object Storage

Resources:

* [Bucket](bucket.yaml)
* [Object](object.yaml)
* [ServiceAccount with static access key](serviceaccount.yaml)


1. Create service account for object storage

```shell
kubectl --context yc-crossplane apply -f infra/kube/yc/examples/objectstorage/serviceaccount.yaml
```

2. Provision Bucket

```shell
kubectl --context yc-crossplane apply -f infra/kube/yc/examples/objectstorage/bucket.yaml
```

3. Create example object

```shell
OBJECT_CONTENT=$(cat infra/kube/yc/examples/objectstorage/example-object.txt | base64)
envsubst < infra/kube/yc/examples/objectstorage/object.yaml | kubectl --context yc-crossplane apply -f -
```

## Further read

* [Application that works with S3](../../../examples/demo-images/http-s3-image)
* [Yandex Cloud doc about Object Storage](https://cloud.yandex.com/en-ru/services/storage)
