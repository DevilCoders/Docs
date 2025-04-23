# Status
Статус: На рассмотрении.

Мотивация:
  * Пока у нас нет промышленного опыта и все ньюансы не видны.

# Передача управления ресурсами Crossplane

## Сценарий
* Мы запускаем пользовательские k8s кластера в публичных облаках (Azure, AWS, YC) с помощью crossplane.
* Мы предоставляем пользователям интерфейс управления managed ресурсами платформы (Azure, AWS, YC) как ресурсами k8s
  через crossplane/etc

## Проблема
В таком сценарии у нас появляется 2 места из которых мы управляем ресурсами платформы:
* Наш bootstrap кластер из которого мы провиженим k8s с установленным crossplane.
* Пользовательский crossplane кластер.

Управляющие кластера могут пересекаться и конфликтовать при управлении ресурсами.

Например:
  * для создания crossplane кластера мы создали в Azure объект `VNet`  
  как ресурс k8s'а он существует только в bootstrap кластере
  * для создания других объектов в crossplane может потребоваться указывать ссылку на этот объект `VNet`

## Решение
Можно его назвать: self-managed with bootstrap.

**Идея**: после развёртывания пользовательского кластера **полностью** передавать контроль управления ресурсами в него.

## Недостатки
### Lack of central control
Такой подход не позволяет иметь в одном месте целостную картину того, какие облака, кем и как используются. Соответственно сильно усложняться сценарии:
  * проверить настройки клиентов на соответствование требованиям СИБ и аудита
  * централизовано обновлять настройки силами команды crossplane
  * централизовано планировать и предоставлять настройки сетей и VPN
  т.к. не будет целостной картины (или её сложно собрать)

### Referencial compatibility
Развёртывание crossplane `VNet` объекта в crossplane кластере не даст ссылаться на него, если в нём будет использовать [ASO](https://github.com/Azure/azure-service-operator), т.к. он будет рассчитывать на собственные типы объектов.

### Как это выглядит абстрактно
* Перекладываем все объекты из bootstrap кластера в пользовательский.
* Из bootstrap кластера *shallow* затираем все ресурсы. Без реального их удаления.
* Так мы передали управление в пользовательский кластер. И больше не управляем ресурсами из 2 мест.

### Как это выглядит на практике
На примере создания пользовательского EKS кластера в AWS.

Мы уже создали EKS кластер со всеми зависимостями для него crossplane ресурсами в bootstrap кластере.

1. Поднимаем provider-aws в пользовательском кластере
```shell
k --context eks create namespace crossplane-system
k --context eks apply -f package/crds
k --context yc get -o yaml deployment -n crossplane-system provider-aws | k --context eks apply -f -
k --context yc get -o yaml secrets -n crossplane-system aws-creds | k --context eks apply -f -
k --context yc get -o yaml providerconfigs.aws.crossplane.io default | k apply -f -
```

2. Перекладываем ресурсы провайдера в aws.

```shell
for RESOURCE in iamrole.identity.aws.crossplane.io/eks-noderole \
  iamrole.identity.aws.crossplane.io/eks-role \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-cluster \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-registry-cni \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-registry-read \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-worker \
  vpc.ec2.aws.crossplane.io/vpc \
  subnet.ec2.aws.crossplane.io/subnet-a \
  subnet.ec2.aws.crossplane.io/subnet-b \
  subnet.ec2.aws.crossplane.io/subnet-c \
  securitygroup.ec2.aws.crossplane.io/sec-group \
  internetgateway.ec2.aws.crossplane.io/internetgateway \
  routetable.ec2.aws.crossplane.io/routetable \
  cluster.eks.aws.crossplane.io/eks \
  nodegroup.eks.aws.crossplane.io/eks-ng-1 \
  nodegroup.eks.aws.crossplane.io/eks-ng-2
do
k --context yc get -o yaml $RESOURCE | k --context eks apply -f -
done
```

3. Удаляем русурсы из bootstrap кластера

* Добавляем в спеки ресурсов `deletionPolicy: Orphan`. Чтобы провайдер не удалял настоящие ресурсы.
* Удаляем ресурсы

```shell

for RESOURCE in iamrole.identity.aws.crossplane.io/eks-noderole \
  iamrole.identity.aws.crossplane.io/eks-role \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-cluster \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-registry-cni \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-registry-read \
  iamrolepolicyattachment.identity.aws.crossplane.io/eks-role-attachment-worker \
  vpc.ec2.aws.crossplane.io/vpc \
  subnet.ec2.aws.crossplane.io/subnet-a \
  subnet.ec2.aws.crossplane.io/subnet-b \
  subnet.ec2.aws.crossplane.io/subnet-c \
  securitygroup.ec2.aws.crossplane.io/sec-group \
  internetgateway.ec2.aws.crossplane.io/internetgateway \
  routetable.ec2.aws.crossplane.io/routetable \
  cluster.eks.aws.crossplane.io/eks \
  nodegroup.eks.aws.crossplane.io/eks-ng-1 \
  nodegroup.eks.aws.crossplane.io/eks-ng-2
do
k --context yc delete $RESOURCE
done
```
