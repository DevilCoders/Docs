# PostgreSQL

В этом примере:

* Создаем RDS postgres instance в одних сетях с EKS
* Выкладываем в EKS приложение, работающее с созданным PostgreSQL

## Prerequisites

* Set up kubernetes environment with crossplane

  You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

* You need [nets](../net) provisioned

## Создание PostgreSQL

Создаем RDS postgres instance со всеми зависимостями:

* [Secret](resources/admin-password.yaml) с админским паролем для postgres
* [DBParameterGroup](resources/params.yaml)
* [DBInstance](resources/instance.yaml)

```shell
kubectl apply -f infra/kube/aws/examples/postgresql/resources
```

Смотри на статусы и дожидаемся создания:

```shell
watch kubectl get -f infra/kube/aws/examples/postgresql/resources
```

Креды (username и password админа) после создания кластера появятся в Secret dbinstance в default namespace'е.

Узнаем endpoint кластера:

```shell
kubectl get -f infra/kube/aws/examples/postgresql/resources/instance.yaml -ojsonpath="{.status.atProvider.endpoint}"
```

## Выкладываем приложение

Для этого создаем:

* [Deployment](app/deployament.yaml)

  В описании Deployment меняем endpoint кластера на созданный нами.

* [LoadBalancer](app/service.yaml)

```shell
kubectl apply -f infra/kube/aws/examples/postgresql/app
```

Дожидаемся создания ресурсов и назначения публичного endpoint'а на LoadBalancer:

```shell
watch kubectl get -f infra/kube/aws/examples/postgresql/app
```

Готово: мы создали RDS postgres Instance и выложили приложение работающее с базой. Заходим по публичному endpoint'у и
проверяем работоспособность приложения.
