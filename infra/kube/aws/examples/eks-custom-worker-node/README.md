# Сценарий
Бывают случаи, когда необходимо добавить специфично настроенную ноду в k8s кластер, которую нельзя настроить с помощью
EKS NodeGroup. В нашем случае это ec2 Instance с IpV6 prefix.

## Prerequisites
Для выполнения инструкций потребуется настроеный EKS кластер с crossplane. Про то как поднять и настроить eks кластер
в [quickstart.md](../../docs/quickstart.md)

## Поднимаем EC2 Instance
Для того, чтобы Instance можно было подключить в кластер нужно:
* Instance должен быть создан в тех же SecurityGroup и Subnet, в которых запущен EKS.
* Для нужно image выбрать образ amazon-eks-node. Например: `ami-0800826177b25080e`.  
Или более актуальный, согласно инструкции [как искать AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html#finding-an-ami-console). Либо через: `aws ec2 describe-images --filter='Name=owner-id,Values=602401143452' --region us-east-1`
* Прописать в `iamInstanceProfile` профиль аналогичный профилю уже существующей NodeGroup
* Добавить тег `kubernetes.io/cluster/eks=owned`
* Добавляем в userData скрипт, который подключит Instance к EKS на старте системы:
```shell
#!/bin/bash
set -o xtrace
/etc/eks/bootstrap.sh eks \
--kubelet-extra-args "--node-labels ipv6-prefix=true --register-with-taints ipv6-prefix=true:NoSchedule"
```

Пример crossplane описания объекта Instance: [eks-worker.yaml](./eks-worker.yaml)

Создаем instance crossplane'ом:
```shell
kubectl apply -f eks-worker.yaml
```

Ждем создания Instance

```shell
watch kubectl get -f eks-worker.yaml
```

Смотрим подключился ли Instance к EKS кластеру.

```shell
kubectl get nodes
```
