# Registry (ECR)

В этом примере:

* Создаем репозиторий в Elastic container registry
* Выдаем права EKS для pull образов из нашего репозитория
* Пушим образ в репозиторий
* Выкладываем приложение с образом из репозитория

## Создаем репозиторий

Ресурсы:

* [Репозиторий](./resources/repo.yaml)

Создаем ресурсы:

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/registry/resources
```

Смотрим статусы, ждем создания:

```shell
watch --context crossplane kubectl get -f infra/kube/aws/examples/registry/resources
```

## Пушим образ

Перед тем как запушить образ настраиваем локальный docker на работу с ECR:

```shell
aws ecr get-login-password --profile aws-infra --region eu-north-1 | \
docker login --username AWS --password-stdin 848727100371.dkr.ecr.eu-north-1.amazonaws.com
```

Пушим образ:

```shell
docker image tag sha256:bca9c3c0384d9e4ef2044bc7a410e7077a23a58e11420e035f613485083e20c2 848727100371.dkr.ecr.eu-north-1.amazonaws.com/static:v0.2
docker image push 848727100371.dkr.ecr.eu-north-1.amazonaws.com/static:v0.2
```

## Выкладываем приложение

Создаем ресурсы Deployment, LoadBalancer:

```shell
kubectl --context eks apply -f infra/kube/aws/examples/registry/app
```

Ждем создания и смотрим на публичный эндпоинт приложения:

```shell
watch kubectl --context eks get -f infra/kube/aws/examples/registry/app
```

Заходим по публичному эндпоинту и проверяем работоспособность приложения.
