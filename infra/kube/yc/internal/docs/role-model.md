# Ролевая модель в Yandex Cloud

Описание модели взаимодействия пользователя с ресурсами облака через Crossplane.

В этой модели пользователь взаимодействует с ресурсами облака не напрямую, а через crossplane. В crossplane пользвоатель
аутентифицируется через персональные уччетные данные, crossplane аутентифицируется в облачной платформе через
ServiceAccount.

User -> Crossplane (Managed Kubernetes in YC) -> Yandex Cloud

## Crossplane -> Yandex Cloud

Crossplane взаимодействует с облачными ресурсами аутентифицируясь через ServiceAccount.

ServiceAccount создается один per folder. Роли на создание ресурсов выдаются на ServiceAccount, роли выдаются в scope
одного folder'а.

Сейчас через crossplane возможны несколько пользовательских сценариев, для каждого сценария нужны свои роли. Подробнее
какие роли нужны для каждого сценария:

* Управление core ресурсами

  В этом случае мы берем частичное управление над ipv6 сетями, folder, cloud и регистрируем их в crossplane ресурсах.
  Нужно разрешить только get на эти ресурсы.

* Управление VM

  В этом случаем необходимо создавать ресурсы Compute Instance. Нужно разрешить get/create/update/delete на эти ресурсы

* Управление KubernetesCluster

  Вместе с созданием kubernetes мы создаем Kubernetes.Cluster, Kubernetes.NodeGroup, KMS.SymmetricKey, ServiceAccount (
  который будет использоваться managed kubernetes'ом), выдаем роли на этот созданный ServiceAccount.

  Нужны get/create/update/delete доступы на эти ресурсы.

* Управление MDB сервисами

  Тут мы создаем PostgreSQL Cluster, MongoDB Cluster, Redis Cluster. Нужны get/create/update/delete доступы на эти
  ресурсы.

  Нужны get/create/update/delete доступы на эти ресурсы.

* Управление Container Registry

  Тут мы создаем ContainerRegistry, Repository.

  Нужны get/create/update/delete доступы на эти ресурсы.

* Управление Object Storage

  Мы создаем Bucket, ServiceAccount, ServiceAccountStaticAccessKey которые используются при создании Bucket.

  Нужны get/create/update/delete доступы на эти ресурсы.

* Управление ролями ServiceAccount'ов

  Для этого случая хочется управлять ролями ServiceAccount'ов через crossplane. Хочется создавать ресурсы
  ServiceAccount, FolderIamBinding или FolderIamMember.

  Для этого тоже нужны get/create/update/delete доступы.

В общем случае crossplane может управлять произвольными ресурсами облака. В случае конкретного пользователя нужны
какие-то определенные сценарии, на которые можно выдать доступы более гранулярно. Эти конкретные сценарии описаны выше.
Т.е. под конкретного пользователя нам не нужна роль admin, если знать целевые сценарии пользователя, то можно выдавать
роли согласно его запросам.

Создание ServiceAccount для crossplane и выдача доступов на него сейчас ручной процесс. ServiceAccount создается один per Fodler.

## User -> Crossplane

Crossplane запущен в Managed Kubernetes сервисе в Yandex Cloud.

Разграничение по tenant'ам происходит через namespace'ы. В конкретном namespace создается ProviderConfig (сущность из
crossplane, описывающая конфигурацию провайдера), к которому привязываются креденшалы ServiceAccount. Область видимости
этих ProviderConfig только в рамках текущего namespace'а. Другими словами технически невозможно привязать ресурсы
текущего namespace'а к ProviderConfig другого namespace'а.

В namespace пользователем создаются ресурсы провайдера (Network, Subnet, VirtualMachine, etc) и привязываются к
ProviderConfig. Так crossplane провайдер отправляет запросы в облачную платформу от имени ServiceAccount указанного в
ProviderConfig.

В Managed Kubernetes пользователь аутентифицируется с персональными credentials.

* Для этого пользователю нужна роль минимальная роль для того, чтобы его учетка приехала в iam folder'а с crossplane (
  resource-manager). После этого authentication-webhook начнет доставлять id пользователя внутрь kubernetes'а. (Сейчас
  это работает через кастомный маппинг в iam-sync)
* И роли на ресурсы выдаются штатными средствами kubernetes через RoleBinding на ресурсы конкретного namespace'а. (
  Сейчас это делается вручную через kubectl apply -f rolebinding.yaml, в котором указываются пользователи поточечно по
  id. Тут было бы удобнее выдавать RoleBinding на группу пользователей, но пока такой возможности нет в Yandex Cloud)
