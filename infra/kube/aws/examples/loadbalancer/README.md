# LoadBalancer (ELB)

// **Status:** work in progress.
Нужно упростить схему создания ELB

## User story

Я хочу, чтобы поды моих приложений были доступны по публичному HTTP(S) эндпоинту, балансер подкладывал ssl сертификат, и
настроить маршрутизацию трафика с одного балансера в разные бэкенды.

## В этом примере:

* Создаем AWS Load Balancer Controller
* Создаем 3 приложения
* Создаем Application Load Balancer поверх приложений с одним публичным эндпоинтом
* Укажем свой сертификат для Application Load Balancer

## Пререквизиты

* [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) - утилита для управления ресурсами kubernetes.
* [helm](https://helm.sh) - интерфейс поверх kubectl, предоставляющий более удобную работу с множеством ресурсов.
* [eksctl](https://eksctl.io) - утилита для создания/управления EKS кластеров и ресурсами вокруг него. В данном примере
  используется для привязки Policy к Service Account в k8s скрывая в одной команде несколько ручных шагов.
* [aws-cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) - утилита для управления
  ресурсами в aws. В данном примере используется для импорта существующего ssl сертификата в Application Load Balancer.

## Создаем AWS Load Balancer Controller

Для аутентификации контроллера в AWS api нужно создать [IAM Policy](./resource/policy.yaml) разрешающую действия с elb
ресурсами:

Создаем:

```shell
kubectl --contex crossplane apply -f inra/kube/aws/examples/loadbalancer/resources/policy.yaml
```

Теперь нужно привязать созданную Policy к ServiceAccount внутри EKS, для этого воспользуемся `eksctl`.

> Для работы `eksctl`:
> * `default` aws profile должен указывать на аккаунт и регион в которых поднят интересующий нас EKS
> * Текущий контекст `kubectl` должен быть выставлен на работу с EKS.

Привязываем Policy:

```shell
eksctl create iamserviceaccount \
  --cluster=eks \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --attach-policy-arn=arn:aws:iam::848727100371:policy/AWSLoadBalancerControllerIAMPolicy \
  --override-existing-serviceaccounts \
  --approve
```

Выкладываем контроллер:

```shell
helm --kube-context eks repo add eks https://aws.github.io/eks-charts
helm --kube-context eks repo update
helm --kube-context eks install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=eks \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller
```

Проверяем успешность установки:

```shell
kubectl --context eks get deployment -n kube-system aws-load-balancer-controller
```

> Для корректной работы контроллера нужно повесить теги:
> * На vpc принадлежащие EKS kubernetes.io/cluster/eks="owned"
> * На публичные subnet принадлежащие EKS kubernetes.io/cluster/eks="owned" kubernetes.io/role/elb="1"
>
> _Если кластер создавался из ресурсов в `infra/kube/aws/resources`, то теги уже должны быть выставлены_

## Создаем самоподписанный ssl сертификат и импортируем его в AWS Certificate Manager

Создаем сертификат на домен example.com:

```shell
openssl req \
  -config infra/kube/aws/examples/elb/certs/crt.cfg -new -x509 -sha256 -newkey rsa:2048 -nodes \
  -keyout infra/kube/aws/examples/elb/certs/example-com.key.pem -days 365 \
  -out infra/kube/aws/examples/elb/certs/example-com.cert.pem
```

Импортируем сертификат в AWS Certificate Manager:

```shell
aws acm import-certificate \
  --certificate fileb://infra/kube/aws/examples/elb/certs/example-com.cert.pem \
  --private-key fileb://infra/kube/aws/examples/elb/certs/example-com.key.pem
```

Запоминаем arn ресурса, укажем его в описании ELB.

## Выкладываем приложение и создаем Application Load Balancer поверх них

Меняем аннотацию `alb.ingress.kubernetes.io/certificate-arn` [Ingress](./app/ingress.yaml)
и указываем в ней arn сертификата полученного на предыдущем шаге.

Создаем:

```shell
kubectl --context eks apply -f infra/kube/aws/examples/loadbalancer/app
```

Смотрим статусы:

```shell
watch kubectl --context eks get -f infra/kube/aws/examples/loadbalancer/app
```

Смотрим карту балансировки:

```shell
kubectl --context eks describe -f infra/kube/aws/examples/elb/loadbalancer/ingress.yaml
```

