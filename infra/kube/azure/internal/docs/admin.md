# Bootstrap control plane for Azure

In this guide we'll:

* Create Azure subscription
* Create ActiveDirectory groups
* Add RoleAssignments with roles approved by Information Security Group on AD groups
* Create namespace and setup Azure Service Operator in Crossplane cluster namespace
* Create and bind Roles to users on ASO resources in Crossplane cluster

## Prerequisites

In this guide we'll use cli tools:

* kubectl - main tool to work with kubernetes
* yc CLI - CLI for Yandex.Cloud
* az CLI - CLI for Azure

[Guide](../../docs/prerequisites.md), how to setup tools. For this guide we need only to setup yc and kubectl on
Crossplane cluster.

## About system

* For users, we provide namespace in Crossplane cluster with deployed and set up ASO.

* Users by themselves can deploy Azure resources via this namespace and ASO. For example users by themselves deploy
  Kubernetes cluster in getting started guide.

* About roles and access management:
    * We use default Azure roles (Can subject do specific action with specific resource?)
    * We bind subsets of roles on Active Directory groups (DevOps, Developer, Contributor for each subscription).
    * Users can request IDM role for subscription + AD group (DevOps, Developer, etc...).
    * After granting IDM role AD sync will sync given domain user in given Azure AD group with bind Roles.

## Setup guide

1. Create Azure Subscription and AD groups for this subscription.
   ask [kaganovich1@](http://staff.yandex-team.ru/kaganovich1)

```shell
# Save subscription name and AD groups ids in env vars
SUBSCRIPTION_NAME="crossplane-sandbox" # name of created subscription
DEVELOPER_AD="00000000-0000-0000-0000-000000000000" # id of created developer AD group
DEVOPS_AD="00000000-0000-0000-0000-000000000000" # id of created devops AD group
CONTRIBUTOR_AD="00000000-0000-0000-0000-000000000000" #id of created contributor AD group>
```

2. Create namespace in Crossplane cluster

```shell
kubectl --context yc-crossplane create namespace $SUBSCRIPTION_NAME
```

3. Setup ASO for new namespace via [guide](aso.md).

4. Apply RoleBindings on ASO resources in Crossplane cluster

Read guide in [infra/kube/azure/internal/rbac](../rbac)

5. Apply default RoleAssignment on Azure subscription.

```shell
SUBSCRIPTION_ID=$(az account list --query "[?name=='$SUBSCRIPTION_NAME'][].{subscriptionId:id}[0]" -o json | jq -r .subscriptionId)

eval "echo \"$(cat infra/kube/azure/internal/roles/rg.yaml infra/kube/azure/internal/roles/contributor.yaml infra/kube/azure/internal/roles/devops.yaml infra/kube/azure/internal/roles/developer.yaml)\"" | kubectl --context yc-crossplane apply -f -
```

6. Substitute SUBSCRIPTION_NAME in template and send answer to users in "Cloud request ticket".

EN

```md
Hello!

We've created Azure subscription for you '$SUBSCRIPTION_NAME' and finished initial setup. Now you can login
in [Azure UI](http://portal.azure.com/) and log in via SSO. There you can find '$SUBSCRIPTION_NAME' subscription.

Next steps:

1. Read [getting started guide](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/azure/docs/user.md) about first
   steps in infrastructure provisioning in Azure.

   In guide you'll find variable SUBSCRIPTION_NAME, use '$SUBSCRIPTION_NAME'

2. Deploy your first application in Azure
3. If you are still have questions ask [vaspahomov@](https://staff.yandex-team.ru/vaspahomov)
```

RU

```md
Привет!

Мы создали для вас подписку в Azure '$SUBSCRIPTION_NAME' и закончили предварительную подготовку. Теперь вы сможете зайти
в [Azure UI](http://portal.azure.com/) и залогиниться через SSO. Там вы сможете найти подписку '$SUBSCRIPTION_NAME'

Дальнейшие шаги:

1. Прочитать [getting started гайд](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/azure/docs/user.md) по первым
   шагам в запуске инфраструктуры в Azure.

   В гайде вы встретите переменную SUBSCRIPTION_NAME, используйте '$SUBSCRIPTION_NAME'

2. Запустить свое первое приложение в Azure
3. Если у вас остались вопросы, спрашивайте [vaspahomov@](https://staff.yandex-team.ru/vaspahomov)
```
