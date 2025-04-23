# ASO

[Getting started guide from azure.](https://azure.github.io/azure-service-operator/)

## Why use Azure Service Operator v2?

* K8s Native: we provide CRDs and Golang API structures to deploy and manage Azure resources through Kubernetes.
* Azure Native: our CRDs understand Azure resource lifecycle and model it using K8s garbage collection via ownership
  references.
* Cloud Scale: we generate K8s CRDs from Azure Resource Manager schemas to move as fast as Azure.
* Async Reconciliation: we don’t block on resource creation.

## [Supported resources](https://azure.github.io/azure-service-operator/introduction/resources/)

* VirtualMachine
* Kubernetes
* MySQL
* Redis
* PostgreSQL
* MongoDB
* LoadBalancer
* SecurityGroup
* VirtualNetwork
* Subnet
* NetworkPeering
* NetworkGateway
* Storage account (aka object storage)

## Install ASO (Azure Service Operator)

### Install cert manager

```
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.yaml
```

### Create service principal and grant roles

* Query info of subscription that you want to work with

```shell
# Set your subscription name here
export SUBSCRIPTION_NAME=crossplane-sandbox
# Deploy ASO in namespace named same as subscription
export TARGET_NAMESPACE=$SUBSCRIPTION_NAME

export SUBSCRIPTION=$(az account list --query "[?name=='$SUBSCRIPTION_NAME'][].{subscriptionId:id,tenantId:tenantId}[0]" -o json)
export AZURE_TENANT_ID=$(echo $SUBSCRIPTION | jq -r .tenantId)
export AZURE_SUBSCRIPTION_ID=$(echo $SUBSCRIPTION | jq -r .subscriptionId)
```

* Create service principal

```shell
# Create service principal
export SERVICE_PRINCIPAL=$(az ad sp create-for-rbac -n "azure-service-operator" --role contributor \
    --scopes /subscriptions/$AZURE_SUBSCRIPTION_ID -o json)
export AZURE_CLIENT_ID=$(echo $SERVICE_PRINCIPAL | jq -r .appId)
export AZURE_CLIENT_SECRET=$(echo $SERVICE_PRINCIPAL | jq -r .password)
```

* Create ASO secret

```shell
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: aso-controller-settings
  namespace: $TARGET_NAMESPACE
stringData:
  AZURE_SUBSCRIPTION_ID: "$AZURE_SUBSCRIPTION_ID"
  AZURE_TENANT_ID: "$AZURE_TENANT_ID"
  AZURE_CLIENT_ID: "$AZURE_CLIENT_ID"
  AZURE_CLIENT_SECRET: "$AZURE_CLIENT_SECRET"
  AZURE_TARGET_NAMESPACES: "$TARGET_NAMESPACE"
EOF
```

* Deploy ASO

```shell
kubectl apply -f https://github.com/Azure/azure-service-operator/releases/download/v2.0.0-alpha.5/multitenant-cluster_v2.0.0-alpha.5.yaml
```

* Configure ASO per namespace

```shell
envsubst < internal/aso/* | k apply -f -
```

### Check deployment succeeded

```shell
kubectl get pods -n azureserviceoperator-system

NAME                                                      READY   STATUS    RESTARTS   AGE
azureserviceoperator-controller-manager-569966545-lctm2   2/2     Running   0          2m20s

kubectl get pods -n $TARGET_NAMESPACE

NAME                                                       READY   STATUS    RESTARTS   AGE
azureserviceoperator-controller-manager-657948696b-bqmwc   1/1     Running   0          12m
```

Now we have deployed ASO, and you can explore [examples](../examples).
