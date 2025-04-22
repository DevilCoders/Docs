# Аутентификация IAM пользователей в EKS

## Задача

Аутентифицировать IAM user и выдать доступ к ресурсам в EKS.

## Инструкция

В ванильном k8s есть интерфейс для добавления аутентифицирующего
webhook. [WebhookTokenAuthentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication)
EKS предоставляет реализует этот интерфейс и предоставляет пользователю интерфейс подмены ответов webhook'а.

Описание ответа хранится в ConfigMap aws-auth в namespace kube-system.
Посмотрим содержимое:

```shell
kubectl get configmap -n kube-system aws-auth -o yaml
```

Для добавления ответа новому IAM user'у:

* Добавим с помощью `kubectl edit configmap -n kube-system aws-auth` в секцию `mapUsers`

```yaml
- userarn: arn:aws:iam::<account-id>:user/<iam-username>
  username: <k8-username>
  groups:
      - <k8s-group>
```

С помощью такой конфигурации auth-webhook начнет аутентифицировать IAM user'а с описанными username и groups

[**Подробная инструкция от AWS.**](https://docs.aws.amazon.com/eks/latest/userguide/add-user-role.html)

