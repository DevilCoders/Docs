# Управление секретами в публичных облаках

### Сценарии по работе с секретами:

* Создать секрет, донести его до разных куберов (control-plane, testing, prod)
* Засинкать crossplane'овский connection details секрет из control-plane в (prod/testing куберы)
* Безопасно хранить секреты в кубе
* Доносить секреты из внутрияндексового YAV в Kubernetes

### Решение

Использовать [Vault](http://vaultproject.io/) как единый control-plane для управления секретами. Vault поднимается в
kubernetes кластере helm chart'ом.

В data-plane (кластера кубернетеса потенциально в разных AWS аккаунтах) доставлять секреты
через [external-secrets-operator](https://external-secrets.io/v0.5.2/). External-secrets подключается к единому Vault.

К каждому Kubernetes подключать KMS, для того чтобы не хранить secrets plain-text'ом в ETCD.

### Pros

* Есть единая (для всех kubernetes кластеров) точка управления секретами (Vault)
* crossplane умеет писать connection-details напрямую в Vault
* В external-secrets-operator есть точка для расширения, чтобы заменить Vault на
  внутренний [YAV](http://yav.yandex-team.ru/)
* В Vault можно ограничить scope доступа на токены
  через [Policy](https://learn.hashicorp.com/tutorials/vault/getting-started-policies).
  Пример: На токен, выданный под testing кластер можно ограничить доступ на префикс /testing

### Незакрытые вопросы

* Как подключать external-secrets-operator ко внешним kubernetes кластерам. (в другой VPC / в другом AWS account)
  Передавать секреты по интернету может быть страшно, даже учитывая то, что Vault к этому готов. Теоретически возможно
  протянуть сетевую связность между разными VPC / account средствами AWS.

### Как поднять

#### Поднимаем Vault.

Нам потребуются уже существующие PostgreSQL, KMS ключ. Создать их можно через crossplane, как именно - можно прочитать в
наших доках в `arcadia/infra/kube`.

Создаем секреты для vault.

```shell
kubectl create secret -n vault generic vault-creds \
--from-literal=AWS_ACCESS_KEY_ID='' \
--from-literal=AWS_SECRET_ACCESS_KEY='' \
--from-literal=VAULT_PG_CONNECTION_URL='' \
--from-literal=PGHOST='' \
--from-literal=PGUSER='' \
--from-literal=PGPASSWORD='' \
--from-literal=VAULT_AWSKMS_SEAL_KEY_ID='5f6c3243-3158-436e-bdf4-ef90d1120ee5' \
--from-literal=VAULT_SEAL_TYPE='awskms'

kubectl create configmap vault-init.sql -n vault --from-literal sqlCommand='
CREATE TABLE IF NOT EXISTS vault_kv_store (
parent_path TEXT COLLATE "C" NOT NULL,
path        TEXT COLLATE "C",
key         TEXT COLLATE "C",
value       BYTEA,
CONSTRAINT pkey PRIMARY KEY (path, key)
);

CREATE INDEX IF NOT EXISTS parent_path_idx ON vault_kv_store (parent_path);

CREATE TABLE IF NOT EXISTS vault_ha_locks (
ha_key                                      TEXT COLLATE "C" NOT NULL,
ha_identity                                 TEXT COLLATE "C" NOT NULL,
ha_value                                    TEXT COLLATE "C",
valid_until                                 TIMESTAMP WITH TIME ZONE NOT NULL,
CONSTRAINT ha_key PRIMARY KEY (ha_key)
);'
```

Заходим через psql в PostgreSQL и создаем Database vault.

Устанавливаем helm chart по [helm-vault-values.yaml](helm-vault-values.yaml)

```shell
helm repo add hashicorp https://helm.releases.hashicorp.com
helm install vault hashicorp/vault --namespace vault -f helm-vault-values.yaml
```

Инициализируем Vault. Не забываем сохранить stdout с рутовым токеном.

```shell
kubectl exec --stdin=true --tty=true -n vault vault-0 -- vault operator init
```

#### AWS IAM auth

Создаем policy разрешающую читать `example_*` секреты.

```shell
vault policy write "example-policy" -<<EOF
path "secret/example_*" {
capabilities = ["create", "read"]
}
EOF
```

Создаем Role в Vault привязанную к example-policy и arn:aws:iam::848727100371:user/vaspahomov пользователю.

```shell
vault write auth/aws/role/dev-role-iam auth_type=iam bound_iam_principal_arn="arn:aws:iam::848727100371:user/vaspahomov" policies=example-policy ttl=5m
```

Логинимся через vault cli. Полученный токен можно использовать в UI.

```shell
vault login -method=aws role=dev-role-iam
```

#### Kubernetes Auth

```shell
vault auth enable kubernetes

export K8S_VAULT_SA_SECRET=$(kubectl get serviceaccount -n external-secrets external-secrets -o json | jq -r '.secrets[0].name')
kubectl get secret ${K8S_VAULT_SA_SECRET} -n external-secrets -o json | jq -r '.data["ca.crt"]' | base64 -d > k8s_ca.crt
kubectl get secret ${K8S_VAULT_SA_SECRET} -n external-secrets -o json | jq -r '.data["token"]' | base64 -d  > vault_sa.token

vault write auth/kubernetes/config \
    token_reviewer_jwt=@vault_sa.token \
    kubernetes_host=https://kubernetes.default.svc \
    kubernetes_ca_cert=@k8s_ca.crt

vault write auth/kubernetes/role/demo \
    bound_service_account_names=* \
    bound_service_account_namespaces=* \
    policies=example-policy \
    ttl=1h
```

#### Поднимаем External-Secrets-Operator

Устанавливем helm chart:

```shell
helm repo add external-secrets https://charts.external-secrets.io
helm repo update
helm install external-secrets external-secrets/external-secrets
```

Складываем рутовый токен от Vault в секрет.

```shell
kubectl create secret generic vault-token -n vault --from-literal 'vault-token=<your-token>'
```

Создаем [ClusterSecretStore](secrets-store.yaml)
Не забываем поменять server url на нужный, найти правильный можно вот так:

```
kubectl get service -n vault vault
```

Создаем:

```shell
kubectl apply -f secrets-store.yaml
```

That's all! мы настроили Vault и External secrets operator.

Пример синхронизации секрета из Vault в Kubernetes: [external-secret.yaml](external-secret.yaml)
