# Проблематика
В системе, особенно с несколькими тенантами, нужно уметь квотировать ресурсы:
  * количество объектов, которые создают пользователи
  * количество ресурсов, которые "потребляют" объекты

Например:
>Я как администратор сервиса хочу ограничить количество сервисов (объектов `Service`) в каждом namespace'е 1000ей.

>Я как провайдер ресурса хочу ограничить кол-во узлов (nodes), которые могут потреблять кластеры AKS и сами VM'ы.

Две этих user story дают разные стратегии решения.

# Count quota
Согласно [официальной документации](https://kubernetes.io/docs/concepts/policy/resource-quotas/), можно ограничивать 
количество кастомных объектов с помощью встроенных механизмов (`--enable-admission-plugins=ResourceQuota`):
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-resources
spec:
  hard:
    count/aksclusters.compute.azure.crossplane.io: 4
```


# Admission controller
Объект `ResourceQuota` достаточно гибкий и позволяет передать _intent_ администратора, например:
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-resources
spec:
  hard:
    count/virtualmachines.compute.azure.crossplane.io: 10
```
Нужен активный _контроллер_, который будет ограничивать потребление. Контроллер может работать:
  * в процессе api server'а (недоступно, т.к. ориентируемся на "ванильный" сервер)
  * в процессе aggregated api server'а (но мы пока не пользуемся)
  * в процессе, к которому api server обращается с webhook'ом.

Предлагается использовать этот механизм. В [официальной документации](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks) есть примеры таких интеграций и базовый код.

Так же в [kubebuilder book](https://book.kubebuilder.io/reference/admission-webhook.html) есть примеры и описание.