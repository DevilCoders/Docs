# Azure Container Registry

**NOTE: ASO does not support Container Registry yet, deploying via az cli**

## Provision

```shell
# Name should be globally unique
REGISTRY_NAME=container-registry

az group create --name registry-rg --location eastus
RESPONSE=$(az acr create --resource-group registry-rg --name container-registry --sku Basic)

echo "Registry URL: '$(echo $RESPONSE | jq -r .loginServer)'"
```

## Adding local config

```shell
az acr login --name container-registry
```

## Setup integration with AKS

```shell
az aks update -n <aks cluster name> -g <aks cluster resource group> --attach-acr container-registry
```

After this step we'll have docker credentials inside kubernetes. And can pull any image from this registry.
