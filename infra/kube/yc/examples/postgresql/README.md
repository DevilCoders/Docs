# Provision PostgreSQL

In this example we'll provision PostgreSQL mdb service

## Prerequisites

* Set up kubernetes environment with crossplane
* Reconciled core resources

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision PostgreSQL

1. Read [Cluster](cluster.yaml) resource and apply your changes in specs

2. Choose password and apply them in kubernetes secret

```shell
export PASSWORD=$(echo 'my-secure-password' | tr -d '\n' | base64)
cat infra/kube/yc/examples/postgresql/*.yaml | envsubst | kubectl --context yc-crossplane apply -f -
```

3. Check resources statuses. Wait then both SYNCED and READY becomes True:

```shell
kubectl --context yc-crossplane get -f infra/kube/yc/examples/postgresql
```

4. After provisioning you can read connection details from kubernetes secret

```shell
kubectl --context yc-crossplane get secret postgress-conn
```

## Further read

* [Deploy application that works with PostgreSQL](../../../examples/deployments/postgresql)
* [Yandex Cloud doc about PostgreSQL](https://cloud.yandex.com/en-ru/services/managed-postgresql)
