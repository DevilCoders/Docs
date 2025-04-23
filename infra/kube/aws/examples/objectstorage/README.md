# Пример S3 выкладки приложения

В этом примере:

* Создаем приватный s3 bucket
* Раздаем service account'у внутри EKS права на работу с s3
* Выкладываем в EKS приложение, работающее с созданным bucket

## Создание s3

* Создаем приватный bucket

О том, что это приватный bucket говорит настройка `spec.forProvider.acl=private`

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/objectstorage/resources/bucket.yaml
```

* Раздаем права на операции с объектами bucket'а service account'у в eks

Для этого создаем:

* [OpenIDConnectProvider](resources/policy/oidc-provider.yaml) для EKS
* [Policy](resources/policy/policy.yaml) разрешающее любые операции
* [IAM Role](resources/policy/role.yaml) для service account в EKS
* [Role Policy Attachment](resources/policy/role.yaml) для того, чтобы привязать Policy к IAM Role service account'а

Создаем:

```shell
export ACCOUNT_ID=141557684765

# Set name and region of EKS
export REGION=eu-north-1
export EKS_NAME=eks

# Set name and namespace of service account in EKS
export SA_NAMESPACE=default
export SA_NAME=s3-sa

export THUMBPRINT=$(./infra/kube/aws/examples/objectstorage/oidc-thumbprint.sh $EKS_NAME $REGION)
export OIDC_URL=$(kubectl --context crossplane get -f infra/kube/aws/examples/kubernetes/cluster.yaml -o json | jq -r '.status.atProvider.identity[0].oidc[0].issuer' | cut -c 9-)
cat infra/kube/aws/examples/objectstorage/resources/policy/* | envsubst | kubectl --context crossplane apply -f -
```

## Выкладываем приложение

* Создаем ServiceAccount с правами на работу с s3

В моем примере это s3-sa в default namespace'е

```shell
kubectl create serviceaccount s3-sa
```

Так как мы уже создали IAM Role привязанную к ServiceAccount default:s3-sa. У созданого sa будут права на работу с s3.

* Создаем объекты deployment/service для нашего приложения

Для deployment указываем ServiceAccount s3-sa, чтобы deployment работал от имени этого sa.

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/objectstorage/deployment
```

* Проверяем состояние ресурсов:

```shell
kubectl --context crossplane get -f infra/kube/aws/examples/objectstorage/deployment
```

Находим публичный эндпоинт нашего приложения в статусе.
