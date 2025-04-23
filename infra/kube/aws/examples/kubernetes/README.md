## Kubernetes (EKS)

In this example we'll:

* Deploy EKS (Elastic Kubernetes Services) cluster, managed kubernetes in AWS
* Setup kubectl config for deployed EKS

## Prerequisites

* Set up kubernetes environment with crossplane
* Set up aws cli locally

  You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

* You need [nets](../net) and [roles](../iamrole) provisioned

## Provision

Deploy kubernetes cluster with all needed dependencies.

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/kubernetes
```

## Connect

* Setup kubeconfig for deployed EKS

```shell
aws eks --region us-east-1 update-kubeconfig --name eks --alias eks
```

* Check setup. Command should show cluster endpoint.

```shell
kubectl --context eks cluster-info
```

## Setup Auth Webhook for EKS

There
are [WebhookTokenAuthentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication)
interface in Kubernetes. For EKS you can setup their behavior.

Configuration stored in aws-auth ConfigMap. Let's look at the current configuration:

```shell
kubectl --context eks get configmap -n kube-system aws-auth -o yaml
```

If you want to setup webhook response for new user you should:

* Add new user with `kubectl --context eks edit configmap -n kube-system aws-auth` in `mapUsers` section like:

```yaml
-   userarn: arn:aws:iam::<account-id>:user/<iam-username>
    username: <k8-username>
    groups:
        - <k8s-group>
```

In this configuration auth-webhook will authenticate IAM user'а with described username и groups

[**Detailed guide from AWS.**](https://docs.aws.amazon.com/eks/latest/userguide/add-user-role.html)


