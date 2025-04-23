# Provision infrastructure in Yandex Cloud

In this guide we'll:

* Create cloud in Yandex.Cloud
* Provision core resources
* Setup crossplane environment

## Prerequisites

You need to set up local environment. Follow [guide](../../docs/local-environment.md).

## Request cloud and nets with yandex connectivity

* Request cloud creation via [form](https://st.yandex-team.ru/createTicket?queue=YCLOUD&_form=10983)
* Request ipv6 connectivity via [form](https://st.yandex-team.ru/createTicket?queue=CLOUD&_form=54816)

## Create crossplane namespace for users

```shell
export FOLDER_NAME=<choose-folder-name-for-user>
# Example
# FOLDER_NAME=crossplane-prod
# FOLDER_NAME=crossplane-preprod
# FOLDER_NAME=taxi-prod
export USER_NAMESPACE=$FOLDER_NAME

# Create namespace and save spec
cd infra/kube/internal/namespaces && ./create-ns.sh $USER_NAMESPACE && cd -
```

## Grant access and provide credentials to your cloud

Base directory should be `infra/kube/yc`.

Create provider config for your own cloud and folder.

```shell
yc resource-manager cloud list --profile prod-fed-user

# Found your prod cloud id in output of last command
PROD_CLOUD_ID="<your prod cloud id>"

yc resource-manager folder list \
  --cloud-id "$PROD_CLOUD_ID" \
  --profile prod-fed-user

# Found your prod folder id in output of last command
PROD_FOLDER_ID="<your prod folder id>"

PROD_SA=$(yc iam service-account create \
  --name prod-crossplane-sa \
  --description "Prod service account for Crossplane" \
  --folder-id "$PROD_FOLDER_ID" \
  --format json)


PROD_SERVICE_ACCOUNT_ID=$(echo "$PROD_SA" | jq -r .id )

# Add editor role to crossplane service account to allow resources management
yc resource-manager folder add-access-binding "$PROD_FOLDER_ID" \
  --role editor \
  --subject "serviceAccount:$PROD_SERVICE_ACCOUNT_ID"
# Add iam.serviceAccounts.admin role to crossplane service account to allow ServiceAccounts management
yc resource-manager folder add-access-binding "$PROD_FOLDER_ID" \
  --role iam.serviceAccounts.admin \
  --subject "serviceAccount:$PROD_SERVICE_ACCOUNT_ID"

yc iam key create \
  --service-account-id $PROD_SERVICE_ACCOUNT_ID \
  --folder-id "$PROD_FOLDER_ID" \
  --output /tmp/prod-crossplane-sa.key

export BASE64ENCODED_PROD_CROSSPLANE_SA_KEY=$(base64 /tmp/prod-crossplane-sa.key | tr -d "\n")
# !!!TODO: rename or change resources namespaces!!!
envsubst < core/providerconfig.yaml | kubectl --context yc-crossplane -n $USER_NAMESPACE apply -f -
```

## Reconcile existing resources: Folder, Network, ipv6 Subnets

```shell
export FOLDER_ID="$PROD_FOLDER_ID"
envsubst < core/folder.yaml | kubectl --context yc-crossplane -n $USER_NAMESPACE apply -f -

yc vpc network list \
--cloud-id "$PROD_CLOUD_ID" \
--folder-id "$PROD_FOLDER_ID" \
--profile prod-fed-user
# Found your prod network id in output of last command
export NETWORK_ID="<your prod network id>"

yc vpc subnet list \
--cloud-id "$PROD_CLOUD_ID" \
--folder-id "$PROD_FOLDER_ID" \
--profile prod-fed-user
# Found your prod subnets ids in output of last command
export SUBNET_A_ID="<your prod subnet id in location a>"
export SUBNET_B_ID="<your prod subnet id in location b>"
export SUBNET_C_ID="<your prod subnet id in location c>"

envsubst < core/nets.yaml | kubectl --context yc-crossplane -n $USER_NAMESPACE apply -f -
```

## Grant access in crossplane namespace for users

[Read guide in RBAC doc](../rbac/README.md)
