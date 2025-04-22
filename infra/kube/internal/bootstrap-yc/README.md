# Bootstrap main crossplane cluster

### Get and export personal access token

```shell
export YC_TOKEN=$(yc iam create-token \
  --profile prod-fed-user \
  --format=json | jq -r .iam_token)
```

### Boostrap kubernetes in preprod folder

* Create new folder in yandex cloud console

* Set cloud id and folder id in [preprod/provider.tf](preprod/provider.tf)

* Apply terraform resources

```shell
cd preprod/terraform
terraform init && terraform apply
```

### Enable egress nat in cloud console (UI)

Egress nat in terraform: [CLOUD-65404](https://st.yandex-team.ru/CLOUD-65404)

### Get kubectl config

```shell
yc managed-kubernetes cluster get-credentials --folder-id b1gj2tg21doe4mcdr530 --external --context-name=yc-crossplane-preprod --name=crossplane-preprod --force
```

### Install helm chart with crossplane

```shell
kubectl create namespace crossplane-system

helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update

# !!!Attention!!! use latest crossplane version. For now 1.5.1
helm install crossplane --namespace crossplane-system crossplane-stable/crossplane --version 1.5.1
```

### Install provider-jet-yc

```shell
kubectl crossplane install provider cr.yandex/crp0kch415f0lke009ft/crossplane/provider-jet-yc:v0.1.5
```

### Reconcile terraform created resources with crossplane

* Create key for provider-jet-yc service account

```shell
yc iam key create --service-account-name=provider-jet-yc-preprod --output key.json --folder-name=crossplane-preprod --output /tmp/prod-crossplane-sa.key
```

* Update resource ids in [core](preprod/core)

* Apply resources

```shell
export BASE64ENCODED_PREPROD_CROSSPLANE_SA_KEY=$(base64 /tmp/prod-crossplane-sa.key | tr -d "\n")
envsubst < preprod/core/providerconfig.yaml | kubectl apply -f -
kubectl apply -f preprod/core/folder.yaml
kubectl apply -f preprod/core/nets.yaml
```
