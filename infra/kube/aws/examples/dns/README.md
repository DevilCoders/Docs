# DNS (Route 53)

## User story

Я хочу начать хостить свои dns зоны в managed сервисе в AWS

## В этом примере:

С помощью crossplane

* Создаем HostedZone в aws
* Создаем dns запись в этой зоне

## Создаем HostedZone

В этом примере создаем зону `asdfaskdlfjaslkdf-crossplane-based-zone.example`

* Указываем имя зоны в [zone.yaml](resources/zone.yaml) в `spec.name.forProvider`.
* Создаем зону

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/dns/resources/zone.yaml
```

## Создаем запись в созданной зоне

В этом примере создадим `CNAME` запись `example` в созданной зоне указывающую на момент написание доки на эндпоинт
Application Load Balancer.

Изменяем интересующие нам поля в [record.yaml](resources/record.yaml)

* В `metadata.name` указываем имя записи. (В нашем случае `example.asdfaskdlfjaslkdf-crossplane-based-zone.example`)
* В `spec.forProvider.type` указываем тип записи. (В нашем случае `CNAME`)
* В `spec.forProvider.resourceRecords.value` указываем значение записи. (В нашем случае эндпоинт
  ALB `k8s-default-nginxing-f2f4d623a8-1969402346.eu-north-1.elb.amazonaws.com`)
* Создаем ресурс

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/dns/resources/record.yaml
```

* Смотрим nameserver'а которые раздают нашу зону:

```shell
kubectl --context crossplane get -f infra/kube/aws/examples/dns/resources/record.yaml -ojsonpath="{.status.atProvider.delegationSet.nameServers}"
```

Выход предыдущей команды:

```shell
["ns-19.awsdns-02.com","ns-1546.awsdns-01.co.uk","ns-654.awsdns-17.net","ns-1428.awsdns-50.org"]
```

> Зона в домене .example не будет растягиваться по другим dns серверам
> [wiki .example](https://en.wikipedia.org/wiki/.example)

* Запрашиваем зону у nameserver'а aws, который мы узнали на предыдущем шаге

```shell
nslookup example.asdfaskdlfjaslkdf-crossplane-based-zone.example ns-18.awsdns-02.com
```

Должны получить примерно такой ответ:

```shell
Server:		ns-19.awsdns-02.com
Address:	2600:9000:5300:1300::1#53

example.asdfaskdlfjaslkdf-crossplane-based-zone.example	canonical name = k8s-default-nginxing-f2f4d623a8-1969402346.eu-north-1.elb.amazonaws.com.
```
