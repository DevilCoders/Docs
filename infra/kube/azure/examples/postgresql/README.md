# Provision PostgreSQL

In this example we'll provision managed PostgreSQL

## Prerequisites

## Prerequisites

* Set up kubernetes environment with crossplane
* Set up az cli locally or use Cloud Shell in Azure Portal

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision PostgreSQL

1. Provision core resources

```shell
kubectl --context yc-crossplane apply -f infra/kube/azure/examples/postgresql/rg.yaml
kubectl --context yc-crossplane apply -f infra/kube/azure/examples/postgresql/nets.yaml
```

2. Create Private DNS Zone to associate with PostgreSQL

```shell
az network private-dns zone create --resource-group postgresql-rg --name privatelink.postgres.database.azure.com
az network private-dns link vnet create --resource-group postgresql-rg \
  --zone-name privatelink.postgres.database.azure.com \
  --name example-postgresql-dns-link \
  --virtual-network postgresql-nets \
  --registration-enabled false
```

3. Read [Cluster](server.yaml) resource and apply your changes in specs

4. Choose password and apply them in kubernetes secret

```shell
export PASSWORD=$(echo $RANDOM | md5 | head -c 20; echo)
export SUBSCRIPTION_NAME="<your-subscription-name-here>"
export SUBSCRIPTION_ID=$(az account list --query "[?name=='$SUBSCRIPTION_NAME'][].{subscriptionId:id}[0]" -o json | jq -r .subscriptionId)
envsubst < infra/kube/azure/examples/postgresql/server.yaml | kubectl --context yc-crossplane apply -f -
```

5. Create database

```shell
kubectl --context yc-crossplane apply -f infra/kube/azure/examples/postgresql/database.yaml
```

6. Check resources statuses.

```shell
kubectl --context yc-crossplane get -f infra/kube/azure/examples/postgresql
```

## Clear resources

1. Delete Private DNS Zone and Private Link:

```shell
az network private-dns link vnet delete --resource-group postgresql-rg \
  --zone-name privatelink.postgres.database.azure.com \
  --name example-postgresql-dns-link
az network private-dns zone delete --resource-group postgresql-rg --name privatelink.postgres.database.azure.com
```

2. Delete all other resources:

```shell
kubectl --context yc-crossplane delete -f infra/kube/azure/examples/postgresql
```

## Further read

* [Deploy application that works with PostgreSQL](../../../examples/deployments/postgresql)
* [Azure doc about PostgreSQL](https://docs.microsoft.com/en-us/azure/postgresql/flexible-server/)
