# Kubernetes

In this example we'll:

* Deploy AKS (Azure Kubernetes Services) cluster, managed kubernetes in Azure
* Setup kubectl config for deployed AKS

## Prerequisites

* Set up kubernetes environment with crossplane
* Set up az cli locally or use Cloud Shell in Azure Portal

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision

Deploy kubernetes cluster with all needed dependencies.

```shell
kubectl --context yc-crossplane apply -f infra/kube/azure/examples/kubernetes
```

## Connect

Choose and add kubectl context for needed kubernetes clusters from Azure

List all clusters. Output will be `AZURE_AKS_NAME` in first column and `AZURE_RESOURCE_GROUP` in second.

```
az aks list -o json | jq -r '.[] | "\(.name) \(.resourceGroup)"'
```

For example add context for `kubernetes-cluster` cluster from `kubernetes-rg` resource group

If you running az cli locally:

```shell
AZURE_RESOURCE_GROUP=kubernetes-rg
AZURE_AKS_NAME=kubernetes-cluster
az aks get-credentials --resource-group $AZURE_RESOURCE_GROUP --name $AZURE_AKS_NAME --context aks
```

If you are using Azure cloud shell:

* In Azure cloud shell

```
SUBSCRIPTION_NAME=<Azure subscription name. "Crossplane ABC service team will provide subscription name for you">
AZURE_ACCESS_TOKEN=$(az account get-access-token --query accessToken --output tsv)
SUBSCRIPTION_ID=$(az account list --query "[?name=='$SUBSCRIPTION_NAME'][].{subscriptionId:id}[0]" -o json | jq -r .subscriptionId)
echo $AZURE_ACCESS_TOKEN
echo $SUBSCRIPTION_ID
```

* Then locally

```shell
AZURE_ACCESS_TOKEN=<copy from azure cloud shell>
SUBSCRIPTION_ID=<copy from azure cloud shell>
./infra/kube/azure/get-client-config.sh $AZURE_ACCESS_TOKEN $AZURE_RESOURCE_GROUP $AZURE_AKS_NAME $AZURE_SUBSCRIPTION_ID
```

**Check kubectl setup**

```shell
kubectl --context aks cluster-info
```

Command should show cluster info like:

```shell
Kubernetes control plane is running at https://kubernetes-7f66cf6b.hcp.westus2.azmk8s.io:443
CoreDNS is running at https://kubernetes-7f66cf6b.hcp.westus2.azmk8s.io:443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://kubernetes-7f66cf6b.hcp.westus2.azmk8s.io:443/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## Further read

* [Image of demo application](../../../examples/demo-images/static)
* [Deploy application](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/)
* [Microsoft doc about Azure Kubernetes Service](https://azure.microsoft.com/en-us/services/kubernetes-service)
