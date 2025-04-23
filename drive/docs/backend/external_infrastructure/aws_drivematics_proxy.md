# Развертывание в AWS EKS L3/L4 balancer + L7 balancer + nginx proxy
## Введение
В данной документации рассмотрен пример деплоя drivematics-proxy на бекенд Яндекса, размещенный в Amazon Web Services. 
**Используется инфраструктура AWS EKS + AWS Fargate + Kubernetes + Docker + AWS ECR**

**Путь запроса: beta.vlootkit.cz -> AWS Route53 -> (открытый в интернет) L3/L4 балансер -> L7 (k8s Ingress) балансер -> k8s NodePort service -> k8s pods**

Для управления контейнерами кластеров в AWS имеется 2 варианта:
* Amazon Elastic Container Service (Amazon ECS)
* Amazon Elastic Kubernetes Service (Amazon EKS)

ECS - чисто амазоновское решение, для универсальности в данном случае - оно не подходит. Поэтому выбор падает на EKS. Amazon EKS nodes по стандарту состоят из Amazon EC2 instances

На кластер EKS можно поднять 3 основных вида node:
* Managed node - Infrastructure as a Service (IaaS)
* Self-managed nodes - самостоятельное управление lifecycle всех нод
* AWS Fargate - Container as a Service (CaaS) / бессерверное ядро для вычислений, AWS полностью берет на себя ответственность по управлению/аллоцированию нодами - проще говоря при построении архитектуры с Fargate можно пропускать шаг с нодами - AWS сам выделяет столько ресурсов сколько нужно, а платим мы за конкретное потребление CPU+RAM.

Для создание кластера нужно иметь настроенные eksctl, kubectl, helm (для установки аддона балансера)

## How to deploy our infrastructure?
Рассмотрим пошаговое развертывание
### Создание кластера с Fargate
1. Создаем кластер
```(bash)
eksctl create cluster -f drive/services/drivematics-eks/production.yaml
```

2. Создадим отдельный fargate profile - хорошая практика не запускать в дефолтных неймспейсах наши сервисы
```(bash)
eksctl create fargateprofile \
--cluster drivematics-production \
--name drivematics-proxy-profile \
--namespace drivematics-proxy
```

3. Проверяем
```(bash)
eksctl get fargateprofile \
--cluster drivematics-production \
-o yaml
```
Должны получить подсети в наш stdout 

### AWS ECR + Docker
В данной части поднимем Docker репозиторий в AWS, построим Docker-образ, чтобы далее его использовать уже в нашем Kubernetes deployment для развертывания приложения.

1. Заводим новый Docker registry в AWS ECR (или используем существующий)
Создается в: https://eu-central-1.console.aws.amazon.com/ecr/repositories?region=eu-central-1

2. Раздать на себя (или создать user group и раздать на нее) policy в IAM - AmazonEC2ContainerRegistryFullAccess для доступа к AWS ECR
```(bash)
aws iam attach-user-policy --policy-arn arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryFullAccess --user-name <username>
```

3. Регистрируемся в ECR
```(bash)
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin <AWS_account_id>.dkr.ecr.eu-central-1.amazonaws.com
```

4. Создаем образ
```(bash)
docker build <path_to_dir_with_Dockerfile> -t <ImageName1>:<stable/latest/testing/etc..>
```

5. Создаем TARGET NAME для образа
```(bash)
docker tag <ImageName1>:<stable/latest/testing/etc..> <AWS_account_id>.dkr.ecr.eu-central-1.amazonaws.com/<ImageName1>:<stable/latest/testing/etc..>
```

6. Push
```(bash)
docker push <AWS_account_id>.dkr.ecr.eu-central-1.amazonaws.com/<ImageName1>:<stable/latest/testing/etc..>
```

Если все шаги прошли успешно получаем image

`<AWS_account_id>.dkr.ecr.eu-central-1.amazonaws.com/<ImageName1>:<stable/latest/testing/etc..>`

Который мы будем использовать для нашего kubernetes

### AWS Load Balancer Controller
Специальный аддон, который берет контроль за нашими k8s service - на себя
Для L3/L4 балансировки - нужен k8s Service типа LoadBalancer
Для L7 балансировки - нужен k8s Service типа Ingress

1. Проверяем существует ли policy (AWSLoadBalancerControllerIAMPolicy) в IAM/Policies. Если существует, то идем в шаг 3
2. Создаем policy
Для регионов КРОМЕ AWS GovCloud (US-East) or AWS GovCloud (US-East)
```(bash)
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.1/docs/install/iam_policy.json &&
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json
```
3. Создаем IAM роль для аддона
```(bash)
eksctl create iamserviceaccount \
--cluster=drivematics-production \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--role-name "AmazonEKSLoadBalancerControllerRole" \
--attach-policy-arn=arn:aws:iam::<AWS_account_id>:policy/AWSLoadBalancerControllerIAMPolicy \
--approve
```

4. Создаем OIDC
Проверяем есть ли уже OIDC
```(bash)
aws eks describe-cluster --name drivematics-production --query "cluster.identity.oidc.issuer" --output text
```

```(bash)
aws iam list-open-id-connect-providers | grep <token from previous request (after id/)>
```
Если результат непустой - то OIDC уже есть, и идем к шагу 4
Иначе создаем
```(bash)
eksctl utils associate-iam-oidc-provider --cluster drivematics-production --approve
```

4. Если версия k8s в AWS <= 1.21, то для использования AWS Security Token Service AWS Regional endpoint стоит сделать
```(bash)
kubectl annotate serviceaccount -n kube-system aws-load-balancer-controller \
    eks.amazonaws.com/sts-regional-endpoints=true
```

5. Для следующей установки аддона с Fargate нужно получить vpcId - можно получить так:
```(bash)
aws eks describe-cluster \
--name drivematics-production \
--region eu-central-1 \
--query "cluster.resourcesVpcConfig.vpcId" \
--output text
```

5. Установка аддона через helm (Конкретно для Fargate)
```(bash)
helm repo add eks https://aws.github.io/eks-charts &&
helm repo update &&
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
-n kube-system \
--set clusterName=drivematics-production \
--set serviceAccount.create=false \
--set serviceAccount.name=aws-load-balancer-controller \
--set region=eu-central-1 \
--set vpcId=vpc-<Id>
```

### Kubernetes
Создаем несколько видов yaml конфигурационных файлов для наших выкаток:
* kind: Deployment - объект k8s, представляющий работающее приложение в кластере
* kind: Service - способ объединить поды в полноценный network service и предоставить доступ до заданных подов
* [Optionally] kind: Namespace - объединить сервисы и поды под какой-то 1 неймспейс

Мы используем AWS Load Balancer Controller - поэтому характерно наличие в yaml таких параметров как
```(yaml)
annotations:
  service.beta.kubernetes.io/aws-load-balancer*:
```

Пример описания файлов есть в drive/backend/services/drivematics_proxy

1. После того как создан кластер, нужно проверить что kubectl видит кластер, например командой
```(bash)
kubectl config view
```

2. Далее нужно все yaml файлы запустить на k8s:
```(bash)
kubectl apply -f <name>.yaml
```

3. Проследить что все сервисы/поды вышли в состояние Running:
Apply приложения (в нашем случае nginx) проверяем как:
```(bash)
kubectl get pods -n drivematics-proxy
```

Apply Load balancer (в нашем случае L7 ingress балансер) проверяем как:
```(bash)
kubectl get ingress -n drivematics-proxy
```

### L3/L4 балансер с ALB Target Group и привязкой к домену
#### Создание ALB Target Group
В данном случае приходится прибегнуть к AWS UI, поскольку не найдено информации как заводить L3/L4 балансер в k8s с перенаправлением в L7 Ingress балансер.
Для начала нужно завести AWS Target Group с L7 балансером, в который будет направлять трафик L3/L4 балансер
```(bash)
aws elbv2 create-target-group \
--name drivematics-proxy-alb \
--vpc-id vpc-<id> \
--port 80 \
--target-type alb \
--protocol TCP
```

```(bash)
aws elbv2 register-targets \
--target-group-arn arn:aws:elasticloadbalancing:eu-central-1:<AWS_account_id>:targetgroup/drivematics-proxy-alb/e1862482c5aecc1b \
--targets Id=arn:aws:elasticloadbalancing:eu-central-1:<AWS_account_id>:loadbalancer/app/k8s-drivemat-drivemat-946795019d/adfe0fba22804880,Port=80
```

#### Создание L3/L4 (AWS NLB) балансера через UI
После заведение таргет группы через UI заводим Network Load Balancer [тут](https://eu-central-1.console.aws.amazon.com/ec2/v2/home?region=eu-central-1#LoadBalancers:sort=loadBalancerName)

с такими параметрами:
1. Scheme: Internal
2. IP address type: для IPv6 кластера - Dualstack; для Ipv4 кластера: IPv4
3. VPC: сеть кластера (в данном случае drivematics-production-cluster)
4. Mappings: выбираем все - и выбираем PublicSubnet везде
5. Listeners and routing: делаем 2 listeners - TCP: 80, TCP: 443. Forward to - таргет группа которую создали для ALB

#### Привязка домена через Route53 к L3/L4 балансеру
**TODO описать процесс**
