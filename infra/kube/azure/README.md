# About

KubeRTC - управление облачными ресурсами через интерфейс kubernetes.

* Вы - заказываете создание облака для запуска своих приложений
* Мы - предоставляем возможность управлять инфраструктурой облака. Использую для этого kubectl, с помощью которого вы
  также можете запускать приложения внутри kubernetes.

Т.е. помимо основных объектов Kubernetes (таких как Pod, Deployment и т.д.)
будут доступны:

* Kubernetes
* Databases:
    * MySQL
    * PostgreSQL
    * CosmosDB Mongo
    * CosmosDB SQL
    * Redis
* Compute:
    * VirtualMachine
    * VirtualMachineScaleSet
* Networking:
    * LoadBalancer
    * NetworkSecurityGroup
    * VirtualNetwork
    * VirtualNetworkGateway
    * VirtualNetworksSubnet
    * VirtualNetworksVirtualNetworkPeering
* StorageAccount (Object storage)
* RoleAssignment

[Полный список ресурсов](https://azure.github.io/azure-service-operator/introduction/resources/)

(*) Недостающие объекты могут быть добавлены по запросу.

# Howto

Чтобы развернуть инфраструктуру в Azure нужно:

* Заполнить [форму](https://st.yandex-team.ru/createTicket?queue=KUBERTC&_form=82765)
  По ней администраторы Crossplane RTC создадут облако:
    * Настроят интеграцию staff/IDM -> Azure.
    * Предоставят реквизиты доступа.
* Полученные реквизиты использовать
  для [настройки локального окружения и подъема основных компонентов инфраструктуры](docs/user.md)
