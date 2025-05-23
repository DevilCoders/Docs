# Настройка групп безопасности

Для [групп безопасности](../../../vpc/concepts/security-groups.md) действует принцип «весь трафик, который не разрешен, запрещен». Чтобы кластер работал, необходимо [создать правила](../../../vpc/operations/security-group-add-rule.md) в его группах безопасности, разрешающие:
* [Служебный трафик внутри кластера](#rules-internal).
* [Подключение к сервисам из интернета](#rules-nodes).
* [Подключение к узлам по SSH](#rules-nodes-ssh).
* [Доступ к API {{ k8s }}](#rules-master).

Вы можете задать более детальные правила для групп безопасности, например, разрешающие трафик только в определенных [подсетях](../../../vpc/concepts/network.md#subnet).

Группы безопасности должны быть корректно настроены для всех подсетей, в которых будет размещен [кластер](../../concepts/index.md#kubernetes-cluster). От этого зависит работоспособность и доступность кластера и запущенных в нем сервисов.

Перед изменением списка групп безопасности или настроек входящих в них правил убедитесь, что это не нарушит работу кластера и его групп узлов.

{% note alert %}

Не удаляйте группы безопасности, привязанные к работающему кластеру или группе узлов: это может привести к нарушению их работы и потере данных.

{% endnote %}

## Создать правила для служебного трафика {#rules-internal}

{% note warning %}

Настройка правил для служебного трафика — обязательное условие для работоспособности регионального кластера.

{% endnote %}

1. Добавьте правила для входящего трафика.
   * Для сетевого балансировщика нагрузки:
     * Диапазон портов — `{{ port-any }}`.
     * Протокол — `TCP`.
     * Тип источника — `CIDR`.
     * Назначение — `198.18.235.0/24` и `198.18.248.0/24`.
   * Для передачи служебного трафика между [мастером](../../concepts/index.md#master) и [узлами](../../concepts/index.md#node-group):
     * Диапазон портов — `{{ port-any }}`:
       * Протокол — любой (`Any`).
       * Тип источника — `Группа безопасности`.
       * Группа безопасности — текущая (`Self`).
   * Для передачи трафика между [подами](../../concepts/index.md#pod) и [сервисами](../../concepts/index.md#service):
     * Диапазон портов — `{{ port-any }}`.
     * Протокол — любой (`Any`).
     * Тип источника — `CIDR`.
     * Назначение — укажите диапазоны адресов подсетей, созданных вместе с кластером, например:
       * `10.96.0.0/16`.
       * `10.112.0.0/16`.
   * Для проверки работоспособности узлов с помощью ICMP-запросов из подсетей внутри {{ yandex-cloud }}:
     * Протокол — `ICMP`.
     * Тип источника — `CIDR`.
     * Назначение — диапазоны адресов подсетей внутри {{ yandex-cloud }}, из которых будет осуществляться диагностика кластера, например:
       * `10.0.0.0/8`.
       * `192.168.0.0/16`.
       * `172.16.0.0/12`.
1. Добавьте правило для исходящего трафика, разрешающее хостам кластера подключаться к внешним ресурсам, например, для скачивания образов с Docker Hub или работы с [{{ objstorage-full-name }}](../../tutorials/backup.md):
   * Диапазон портов — `{{ port-any }}`.
   * Протокол — любой (`Any`).
   * Тип источника — `CIDR`.
   * Назначение — `0.0.0.0/0`.

## Создать правило для подключения к сервисам из интернета {#rules-nodes}

Чтобы запущенные на узлах сервисы были доступны из интернета и подсетей внутри {{ yandex-cloud }}, создайте правило для входящего трафика:
* Диапазон портов — `30000-32767`.
* Протокол — `TCP`.
* Тип источника — `CIDR`.
* Назначение — `0.0.0.0/0`.

## Создать правило для подключения к узлам по SSH {#rules-nodes-ssh}

Для подключения к узлам по протоколу SSH создайте правило для входящего трафика:
* Порт — `{{ port-ssh }}`.
* Протокол — `TCP`.
* Тип источника — `CIDR`.
* Назначение — диапазоны адресов подсетей внутри {{ yandex-cloud }}, а также публичные IP-адреса компьютеров в интернете, например:
  * `10.0.0.0/8`.
  * `192.168.0.0/16`.
  * `172.16.0.0/12`.
  * `85.32.32.22/32`.

## Создать правила для доступа к API {{ k8s }} {#rules-master}

Для доступа к API {{ k8s }} и управления кластером с помощью `kubectl` и других утилит нужны правила, разрешающие подключение к мастеру через порты `{{ port-k8s }}` и `{{ port-https }}`. Создайте два правила для входящего трафика, по одному для каждого порта:
* Порты — `{{ port-https }}`, `{{ port-k8s }}`.
* Протокол — `TCP`.
* Тип источника — `CIDR`.
* Назначение — укажите диапазон адресов подсетей, из которых будете управлять кластером, например:
  * `85.23.23.22/32` — для внешней сети.
  * `192.168.0.0/24` — для внутренней сети.

## Примеры {#examples}

{% list tabs %}

- {{ TF }}

  Например, нужно создать правила для имеющегося кластера {{ k8s }}:
  * с зональным мастером, размещенным в зоне доступности `{{ region-id }}-a`;
  * с группой узлов `worker-nodes-с`;
  * с доступом к сервисам:
    * с диапазона адресов балансировщика нагрузки `198.18.235.0/24` и `198.18.248.0/24`;
    * из внутренней подсети `10.129.0.0/24` для передачи трафика между подами и сервисами;
    * из внутренней подсети `172.16.0.0/12` для протокола ICMP;
    * из интернета с любых адресов (`0.0.0.0/0`) на диапазон портов NodePort (`30000-32767`);
  * с доступом к узлам из интернета с адреса `85.32.32.22/32` на порт `{{ port-ssh }}`;
  * с доступом к API {{ k8s }} из внешней подсети с диапазона адресов `203.0.113.0/24` через порты `{{ port-https }}` и `{{ port-k8s }}`.

  Будут созданы четыре группы безопасности:
  * `k8s-main-sg` — правила для служебного трафика;
  * `k8s-public-services` — правила для подключения к узлам из интернета;
  * `k8s-nodes-ssh-access` — правила для подключения к узлам по протоколу SSH;
  * `k8s-master-whitelist`— правила для доступа к API кластера.

  {% cut "Конфигурационный файл для такого кластера:" %}

  {% if product == "yandex-cloud" %}

  ```hcl
  terraform {
    required_providers {
      yandex = {
        source = "yandex-cloud/yandex"
      }
    }
  }

  provider "yandex" {
    token     = "<OAuth или статический ключ сервисного аккаунта>"
    cloud_id  = "<идентификатор облака>"
    folder_id = "<идентификатор каталога>"
    zone      = "<зона доступности>"
  }

  resource "yandex_vpc_security_group" "k8s-main-sg" {
    name        = "k8s-main-sg"
    description = "Правила группы обеспечивают базовую работоспособность кластера. Примените ее к кластеру и группам узлов."
    network_id  = "<идентификатор облачной сети>"
    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает проверки доступности с диапазона адресов балансировщика нагрузки. Нужно для работы отказоустойчивого кластера и сервисов балансировщика."
      v4_cidr_blocks = ["198.18.235.0/24", "198.18.248.0/24"]
      from_port      = 0
      to_port        = 65535
    }
    ingress {
      protocol          = "ANY"
      description       = "Правило разрешает взаимодействие мастер-узел и узел-узел внутри группы безопасности."
      predefined_target = "self_security_group"
      from_port         = 0
      to_port           = 65535
    }
    ingress {
      protocol       = "ANY"
      description    = "Правило разрешает взаимодействие под-под и сервис-сервис. Укажите подсети вашего кластера и сервисов."
      v4_cidr_blocks = ["10.129.0.0/24"]
      from_port      = 0
      to_port        = 65535
    }
    ingress {
      protocol       = "ICMP"
      description    = "Правило разрешает отладочные ICMP-пакеты из внутренних подсетей."
      v4_cidr_blocks = ["172.16.0.0/12"]
    }
    egress {
      protocol       = "ANY"
      description    = "Правило разрешает весь исходящий трафик. Узлы могут связаться с {{ container-registry-full-name }}, {{ objstorage-name }}, Docker Hub и т. д."
      v4_cidr_blocks = ["0.0.0.0/0"]
      from_port      = 0
      to_port        = 65535
    }
  }

  resource "yandex_vpc_security_group" "k8s-public-services" {
    name        = "k8s-public-services"
    description = "Правила группы разрешают подключение к сервисам из интернета. Примените правила только для групп узлов."
    network_id  = "<идентификатор облачной сети>"

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает входящий трафик из интернета на диапазон портов NodePort. Добавьте или измените порты на нужные вам."
      v4_cidr_blocks = ["0.0.0.0/0"]
      from_port      = 30000
      to_port        = 32767
    }
  }

  resource "yandex_vpc_security_group" "k8s-nodes-ssh-access" {
    name        = "k8s-nodes-ssh-access"
    description = "Правила группы разрешают подключение к узлам кластера по SSH. Примените правила только для групп узлов."
    network_id  = "<идентификатор облачной сети>"

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает подключение к узлам по SSH с указанных IP-адресов."
      v4_cidr_blocks = ["85.32.32.22/32"]
      port           = 22
    }
  }

  resource "yandex_vpc_security_group" "k8s-master-whitelist" {
    name        = "k8s-master-whitelist"
    description = "Правила группы разрешают доступ к API {{ k8s }} из интернета. Примените правила только к кластеру."
    network_id  = "<идентификатор облачной сети>"

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает подключение к API {{ k8s }} через порт {{ port-k8s }} из указанной сети."
      v4_cidr_blocks = ["203.0.113.0/24"]
      port           = 6443
    }

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает подключение к API {{ k8s }} через порт {{ port-https }} из указанной сети."
      v4_cidr_blocks = ["203.0.113.0/24"]
      port           = 443
    }
  }

  resource "yandex_kubernetes_cluster" "k8s-cluster" {
    name = "k8s-cluster"
    ...
    master {
      version = "1.20"
      zonal {
        zone      = "{{ region-id }}-a"
        subnet_id = <идентификатор облачной подсети>
      }

      security_group_ids = [
        yandex_vpc_security_group.k8s-main-sg.id,
        yandex_vpc_security_group.k8s-master-whitelist.id
      ]
      ...
    }
    ...
  }

  resource "yandex_kubernetes_node_group" "worker-nodes-с" {
    cluster_id = yandex_kubernetes_cluster.k8s-cluster.id
    name       = "worker-nodes-с"
    version    = "1.20"
    ...
    instance_template {
      platform_id = "standard-v3"
      network_interface {
        nat                = true
        subnet_ids         = [<идентификатор облачной подсети>]
        security_group_ids = [
          yandex_vpc_security_group.k8s-main-sg.id,
          yandex_vpc_security_group.k8s-nodes-ssh-access.id,
          yandex_vpc_security_group.k8s-public-services.id
        ]
        ...
      }
      ...
    }
  }
  ```

  {% endif %}

  {% if product == "cloud-il" %}

  ```hcl
  terraform {
    required_providers {
      yandex = {
        source = "yandex-cloud/yandex"
      }
    }
  }

  provider "yandex" {
    endpoint  = "{{ api-host }}:443"
    token     = "<статический ключ сервисного аккаунта>"
    cloud_id  = "<идентификатор облака>"
    folder_id = "<идентификатор каталога>"
    zone      = "<зона доступности>"
  }

  resource "yandex_vpc_security_group" "k8s-main-sg" {
    name        = "k8s-main-sg"
    description = "Правила группы обеспечивают базовую работоспособность кластера. Примените ее к кластеру и группам узлов."
    network_id  = "<идентификатор облачной сети>"
    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает проверки доступности с диапазона адресов балансировщика нагрузки. Нужно для работы отказоустойчивого кластера и сервисов балансировщика."
      v4_cidr_blocks = ["198.18.235.0/24", "198.18.248.0/24"]
      from_port      = 0
      to_port        = 65535
    }
    ingress {
      protocol          = "ANY"
      description       = "Правило разрешает взаимодействие мастер-узел и узел-узел внутри группы безопасности."
      predefined_target = "self_security_group"
      from_port         = 0
      to_port           = 65535
    }
    ingress {
      protocol       = "ANY"
      description    = "Правило разрешает взаимодействие под-под и сервис-сервис. Укажите подсети вашего кластера и сервисов."
      v4_cidr_blocks = ["10.129.0.0/24"]
      from_port      = 0
      to_port        = 65535
    }
    ingress {
      protocol       = "ICMP"
      description    = "Правило разрешает отладочные ICMP-пакеты из внутренних подсетей."
      v4_cidr_blocks = ["172.16.0.0/12"]
    }
    egress {
      protocol       = "ANY"
      description    = "Правило разрешает весь исходящий трафик. Узлы могут связаться с {{ container-registry-full-name }}, {{ objstorage-name }}, Docker Hub и т. д."
      v4_cidr_blocks = ["0.0.0.0/0"]
      from_port      = 0
      to_port        = 65535
    }
  }

  resource "yandex_vpc_security_group" "k8s-public-services" {
    name        = "k8s-public-services"
    description = "Правила группы разрешают подключение к сервисам из интернета. Примените правила только для групп узлов."
    network_id  = "<идентификатор облачной сети>"

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает входящий трафик из интернета на диапазон портов NodePort. Добавьте или измените порты на нужные вам."
      v4_cidr_blocks = ["0.0.0.0/0"]
      from_port      = 30000
      to_port        = 32767
    }
  }

  resource "yandex_vpc_security_group" "k8s-nodes-ssh-access" {
    name        = "k8s-nodes-ssh-access"
    description = "Правила группы разрешают подключение к узлам кластера по SSH. Примените правила только для групп узлов."
    network_id  = "<идентификатор облачной сети>"

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает подключение к узлам по SSH с указанных IP-адресов."
      v4_cidr_blocks = ["85.32.32.22/32"]
      port           = 22
    }
  }

  resource "yandex_vpc_security_group" "k8s-master-whitelist" {
    name        = "k8s-master-whitelist"
    description = "Правила группы разрешают доступ к API {{ k8s }} из интернета. Примените правила только к кластеру."
    network_id  = "<идентификатор облачной сети>"

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает подключение к API {{ k8s }} через порт {{ port-k8s }} из указанной сети."
      v4_cidr_blocks = ["203.0.113.0/24"]
      port           = 6443
    }

    ingress {
      protocol       = "TCP"
      description    = "Правило разрешает подключение к API {{ k8s }} через порт {{ port-https }} из указанной сети."
      v4_cidr_blocks = ["203.0.113.0/24"]
      port           = 443
    }
  }

  resource "yandex_kubernetes_cluster" "k8s-cluster" {
    name = "k8s-cluster"
    ...
    master {
      version = "1.20"
      zonal {
        zone      = "{{ region-id }}-a"
        subnet_id = <идентификатор облачной подсети>
      }

      security_group_ids = [
        yandex_vpc_security_group.k8s-main-sg.id,
        yandex_vpc_security_group.k8s-master-whitelist.id
      ]
      ...
    }
    ...
  }

  resource "yandex_kubernetes_node_group" "worker-nodes-с" {
    cluster_id = yandex_kubernetes_cluster.k8s-cluster.id
    name       = "worker-nodes-с"
    version    = "1.20"
    ...
    instance_template {
      platform_id = "standard-v3"
      network_interface {
        nat                = true
        subnet_ids         = [<идентификатор облачной подсети>]
        security_group_ids = [
          yandex_vpc_security_group.k8s-main-sg.id,
          yandex_vpc_security_group.k8s-nodes-ssh-access.id,
          yandex_vpc_security_group.k8s-public-services.id
        ]
        ...
      }
      ...
    }
  }
  ```

  {% endif %}

  {% endcut %}

{% endlist %}