# Prerequisites

## Request roles

* Crossplane cluster user role. Ask [vaspahomov@](http://staff.yandex-team.ru/vaspahomov)
* [DevOps role](https://idm.yandex-team.ru/system/cloud-crossplane/roles#rf=1,rf-role=Yw6dgUy5#cloud-crossplane/azure/sandbox/az_devops(fields:()),f-status=all,f-role=cloud-crossplane,sort-by=-updated,rf-expanded=Yw6dgUy5)
  in azure subscription

## Command line tools

For our work with azure we need:

* kubectl - main tool to work with kubernetes
* yc CLI - CLI for Yandex.Cloud
* az CLI - CLI for Azure

### YC CLI

[Yandex cloud's setup manual](https://wiki.yandex-team.ru/cloud/support/tools/#yandex.cloudcliyc)

[Documentation about yc cli](https://cloud.yandex.ru/docs/cli/cli-ref/)

* Install yc cli
  ```shell
  curl https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash
  ```

* Setup profile
  ```shell
  yc config profile create prod-fed-user
  yc config set federation-id yc.yandex-team.federation
  yc config set federation-endpoint console.cloud.yandex.ru
  yc config set compute-default-zone ru-central1-b
  yc config set endpoint api.cloud.yandex.net:443
  ```

* Check setup

  Output should be list of available clouds

  ```shell
  yc resource-manager cloud list
  ```

### AZ CLI

You can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart). Or install and setup az
cli locally:

1. Install using microsoft [guide](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

2. Login in azure from cli.

```shell
# After pressing enter follow instructions: open browser, enter code, login from domain account.
az login
```

3. Set your subscription name:

    ```shell
    SUBSCRIPTION_NAME=<Azure subscription name. "Crossplane ABC service team will provide subscription name for you">
    az account set --subscription "$SUBSCRIPTION_NAME"
    ```

### Kubectl

* Install kubectl

  [official guide](https://kubernetes.io/docs/tasks/tools/#kubectl).

* Setup kubectl context on crossplane cluster

```
export NAMESPACE_NAME='<your-namespace-here>'

yc managed-kubernetes cluster get-credentials \
  --name crossplane \
  --context-name yc-crossplane \
  --folder-name crossplane \
  --cloud-id b1gjk8shtb2smi1cgqdn \
  --profile prod-fed-user \
  --external

kubectl config set-context yc-crossplane --namespace=$NAMESPACE_NAME
```
