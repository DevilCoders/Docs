# Compositions 

## Проблема управления множестом ресуров

Мой сценарий с точки зрения пользователя: 
>Я хочу запустить приложение в Azure.

Для этого мне нужно:
* [Создать AKS](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/examples/aks/aks.yaml) в котором можно запускать сервис, по пути настроив все зависимости
  * [VirtualNetwork](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/examples/aks/net.yaml)
  * [Role, RoleAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/examples/aks/aks-deps.yaml)
* Создать зависимости для приложения
  * [Managed база данных](https://github.com/crossplane/provider-azure/blob/master/examples/database/postgresqlserver.yaml)
  * Настроить мониторинги, etc 
* Задеплоить приложение
  * [Создать k8s Deployment](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/examples/nginx/deployment/deployment.yaml)
  * [Создать k8s Service](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/examples/nginx/deployment/service.yaml), для того чтобы пустить внешний трафик на поды

Как видно из схемы, для самого простого базового пользовательского сценария нужно создавать и управлять множеством ресурсов. 
Если проваливаться в описания объектов можно найти много параметров, которые рядовому пользователю неинтересны. Например: маски VirtualNetwork, Subnet. 

## Способы решения проблемы

* **`kustomize` + `kubectl apply -f .`**

С помощью kustomize решаем проблему избыточных настроек. Пример можно посмотреть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/examples/sandbox/pub)

С помощью `kubectl get/apply -f` решаем проблему управления множеством ресурсов.

* **Composition**
Пишем crossplane Composition, который объединит несколько мелких объектов и подставит неинтересные нам поля. [Пример для AKS](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/compositions/configuration/aks)

## Подробнее про Composition

### Глосарий
* Managed ресурс - crd созданный при установке одного из провайдеров crossplane
* CompositeResourceDefinition - структура ресурса на подобии ванильных k8s CRD.
* Composition - k8s ресурс, который является композицией над managed ресурсами

### Написание Composition

Описываем CompositeResourceDefinition. Описание сильно похоже на ванильный CustomResourceDefinition. [пример](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/compositions/configuration/aks/definition.yaml)

В Composition описывается список ресурсов, вокруг которых мы строим Composition. Для [AzureK8SCluster](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/compositions/configuration/aks/composition.yaml?rev=r8599721) ресурса описываем:
* ResourceGroup
* VirtualNetwork
* Subnet
* AKSCluster
* Role
* RoleAssignment

На примере AKSCluster, посмотрим как описываются шаблоны ресурсов внутри Composition:
```yaml
- name: akscluster
  # В base описываем основной шаблон ресурса
  base:
    apiVersion: compute.azure.crossplane.io/v1alpha3
    kind: AKSCluster
    spec:
      resourceGroupNameSelector:
        matchControllerRef: true
      vnetSubnetIDSelector:
        matchControllerRef: true
      disableRBAC: false
      nodeVMSize: Standard_B2s
      nodeCount: 3
      writeConnectionSecretToRef:
        namespace: crossplane-system
      providerConfigRef:
        name: default
  # В patches описываем патчи в base описание
  patches:
  # С помощью простых from to патчей 
  # описываем как маппить поля из spec Composition'а в spec ресурсов
  - fromFieldPath: "spec.location"
    toFieldPath: "spec.location"
  - fromFieldPath: "spec.version"
    toFieldPath: "spec.version"
  - fromFieldPath: "spec.nodeCount"
    toFieldPath: "spec.nodeCount"
  - fromFieldPath: "spec.nodeVMSize"
    toFieldPath: "spec.nodeVMSize"
  # С помощью transforms можем изменять значение из from перед подстановкой в to
  - fromFieldPath: "metadata.name"
    toFieldPath: "spec.dnsNamePrefix"
    transforms:
    - type: string
        string:
          fmt: "crossplane-%s"
  - fromFieldPath: "metadata.uid"
    toFieldPath: "spec.writeConnectionSecretToRef.name"
    transforms:
    - type: string
        string:
          fmt: "%s-aks"
  # Описываем какие connection details нужно пробросить 
  # из managed ресурса в connection details Composition'а
  connectionDetails:
  - fromConnectionSecretKey: endpoint
  - fromConnectionSecretKey: username
  - fromConnectionSecretKey: password
  - fromConnectionSecretKey: clusterCA
  - fromConnectionSecretKey: clientCert
  - fromConnectionSecretKey: clientKey
  - fromConnectionSecretKey: token
  - fromConnectionSecretKey: kubeconfig
  - fromConnectionSecretKey: principalID
```

Мнение про такие описания. Простых патчей, например переноса поля из spec Composition'а в spec managed ресурса. Все выглядит неплохо.
```yaml
- fromFieldPath: "spec.location"
  toFieldPath: "spec.location"
```

Если же нам нужно что-то чуть более сложное, например отформатировать строку, вид начинает портиться.
```yaml
- fromFieldPath: "metadata.name"
  toFieldPath: "spec.dnsNamePrefix"
  transforms:
  - type: string
      string:
        fmt: "crossplane-%s"
```

Возможности такого описания патчей не безграничны. 
Например, ими не получится выразить конструкцию: сделай insert в список на 3 позицию.

### Отладка при разработке Composition'ов.

При таком хитром патчинге спек достаточно просто ошибиться, например, неправильно указать `toFieldPath`. Из-за этого мы получим объект, который при server-side apply crossplane'ом провалит этап валидации. При этом crossplane не пишет в лог сообщение с ошибкой валидации.

Разработчик не может посмотреть результаты патчинга managed ресурсов. Средствами k8s невозможно получить в человеко-читаемом формате (yaml?) результат патчинга до того, как ресурс реально создастся в кластере, а чтобы это произошло нужно пройти все проверки валидации.

### [Примеры пользовательских конфигураций](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube/compositions/example)

Спека для создания k8s кластера в azure с забутстраплеными crossplane, azure service operator
```yaml
apiVersion: infra.yandex/v1alpha1
kind: CrossplaneCluster
metadata:
  name: demo-aks
  namespace: default
spec:
  location: West US 2
  version: "1.19.11"
  namespace: default
  writeConnectionSecretToRef:
    name: crossplane-cluster-conn
  # overrides
#  nodeCount: 1
#  nodeVMSize: Standard_B2s
```

Спека пользовательского приложения. 

Ресурс нужно создавать в AKS забутстрапленный в azure c помощью CrossplaneCluster. 

При создании такого ресурса. Мы поднимаем ManagedPostgres в azure, k8s Deployment, k8s Service который создаст для себя публичный IP адрес
```yaml
apiVersion: infra.yandex/v1alpha1
kind: PostgresApplication
metadata:
  name: demo-application
  namespace: default
spec:
  postgres:
    storageGB: 10
  deployment:
    image: cr.yandex/crp05dvtcqpakmaeq8hq/http-pg:v0.18
    # overrides. 
    replicas: 1 # default 3
```

### Какие composition'ы есть

* K8SCluster
* Application
* ManagedPostgres

* Helm based
  * CrossplaneRelease
  * AzureServiceOperatorRelease
  * CertManagerRelease
  
  Composition'ы запускающие соответствующие helm releas'ы во внешних k8s кластерах, поднятых crossplane'ом

* CrossplaneCluster
  
  Composition поверх Composition'ов (тут нужна картинка с ДиКаприо из Начало)
  * K8SCluster
  * CrossplaneRelease
  * AzureServiceOperatorRelease
  * CertManagerRelease

* PostgresApplication
  Также Composition поверх Composition'ов
  * ManagedPostgres
  * Application

### Как Composition разворачивается в Managed ресурсы
В отличии от managed ресурсов Composition может быть namespaced объектом. [Multi-Tenant Crossplane](https://github.com/crossplane/crossplane/blob/master/docs/guides/multi-tenant.md)

Namespaced Composition выглядят достаточно странно. Он является claim'ом видя который crossplane создает ему в пару cluster-wide объект дописывая в metadata.name рандомизированный суффикс.

По cluster-wide Composition'ам crossplane создает managed ресурсы. 

Можно отметить неприятный момент - при превращении namespaced cliam'а в cluster wide объект Composition мы теряем поле `metadata.namespace`. Но информация про namespace откладывается в labels. 
```json
❯ kubectl get K8SCluster demo-aks-fpn6l-t2pwv -o json | jq .metadata.labels
{
  "crossplane.io/claim-name": "demo-aks",
  "crossplane.io/claim-namespace": "default",
  "crossplane.io/composite": "demo-aks-fpn6l"
}
```
Чтобы его использовать при патчинге: `fromFieldPath: metadata.labels[crossplane.io/claim-namespace]`

### Как посмотреть статус managed ресурса, если я создавал Composition
Достаточно специфичный кейс. Пользователь не хочет знать про статусы managed объектов по отдельности. Пользователь хочет знать только статус целостного Composition.

Такая потребность возникает и у пользователя, когда "что-то идёт не так". Достаточно посмотреть на обилие тикетов и доработок в Deploy про отображение ошибок.

Как найти managed ресурс по namespaced cliam'у Composition'а?
* `kubectl describe -f crossplane-cluster.yaml`  
  Смотрим в spec.resourceRef для того чтобы по claim'у найти cluster wide объект Composition'а. 
* `kubectl describe CompositeCrossplaneCluster demo-aks-fpn6l`
  Смотрим в spec.resourceRefs для того чтобы найти имена из которых собрана Composition. Но в нашем случае CrossplaneCluster собран из Composition'а K8SCluster, поэтому продолжаем
* `kubectl describe K8SCluster demo-aks-fpn6l-t2pwv`
* `kubectl describe CompositeAzureK8SCluster demo-aks-fpn6l-t2pwv-xqhgp`
* `kubectl describe AKSCluster demo-aks-fpn6l-nc6js `
  Ура! Мы добрались до конца до managed объекта  

### Завершение

В итоге мы получили очень удобный способ для пользователя создавать достаточно специфичные объекты, например, `ManagedPostgres` и  `CrossplaneCluster`.

Но при этом достаточно сложные в разработке и отладке конструкции - т.е. при эксплуатации.

Все было бы суперхорошо, если бы небольшого ограниченного набора Composition'ов хватало пользователям на все случаи жизни. Но, кажется, что это не так:
* PostgresApplication - пользователь может захотеть создать приложение с MySQL базой данных, для этого придется разрабатывать/отлаживать еще один Composition
* Пользователь может захотеть более гибко настроить deployment. Создать 2 контейнера внутри пода. Для этого еще один Composition.
* etc, etc, etc. 
* А дальше декартово произведение и комбинаторный взрыв бесконечного разнообразия желаний пользователей:(