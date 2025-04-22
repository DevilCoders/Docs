# Prerequisites

## Request roles

* Crossplane cluster user role. Ask [vaspahomov@](http://staff.yandex-team.ru/vaspahomov)
* ~~Request access to AWS~~

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

### Kubectl

* Install kubectl

  [official guide](https://kubernetes.io/docs/tasks/tools/#kubectl).

* Setup kubectl context on crossplane cluster

```
export NAMESPACE_NAME='<your-namespace-here>'

yc managed-kubernetes cluster get-credentials \
  --name crossplane \
  --context-name crossplane \
  --folder-name crossplane \
  --cloud-id b1gjk8shtb2smi1cgqdn \
  --profile prod-fed-user \
  --external

kubectl config set-context crossplane --namespace=$NAMESPACE_NAME
```
