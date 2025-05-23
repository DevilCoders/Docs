# Создать виртуальную машину из набора дисков

Создать виртуальную машину можно из существующих дисков. Диски должны находиться в одной из зон доступности и не быть добавленными к другим виртуальным машинам.

{% include [disk-auto-delete](../../_includes_service/disk-auto-delete.md) %}

Чтобы создать виртуальную машину из набора дисков:

{% list tabs %}

- Консоль управления

  Чтобы создать виртуальную машину:
  1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором будет создана виртуальная машина.
  1. В списке сервисов выберите **{{ compute-name }}**.
  1. Нажмите кнопку **Создать ВМ**.
  1. В блоке **Базовые параметры**:
      * Введите имя и описание ВМ. Требования к имени:

          {% include [name-format](../../../_includes/name-format.md) %}

          {% include [name-fqdn](../../../_includes/compute/name-fqdn.md) %}

      * Выберите [зону доступности](../../../overview/concepts/geo-scope.md), в которой будет находиться виртуальная машина.

  1. В блоке **Выбор образа/загрузочного диска** выберите один из [образов](../../operations/images-with-pre-installed-software/get-list.md).

  1. В блоке **Диски{% if product == "yandex-cloud" %} и файловые хранилища{% endif %}** [добавьте диск](./create-from-disks.md):
      * Нажмите кнопку **Добавить диск**.
      * Введите имя диска.
      * Выберите [тип диска](../../concepts/disk.md#disks_types).
      * Укажите нужный размер блока.
      * Укажите нужный размер диска.
      * (опционально) Включите опцию **Удалять вместе с ВМ**, если нужно автоматически удалять диск при удалении ВМ, к которой он будет подключен.
      * Выберите наполнение `Диск`.
      * Нажмите кнопку **Добавить**.

  {% if product == "yandex-cloud" %}
  1. (опционально) В блоке **Диски и файловые хранилища** на вкладке **Файловые хранилища** подключите [файловое хранилище](../../concepts/filesystem.md):
      * Нажмите кнопку **Подключить файловое хранилище**.
      * В открывшемся окне выберите файловое хранилище.
      * Введите имя устройства.
      * Нажмите кнопку **Подключить файловое хранилище**.
  {% endif %}

  1. В блоке **Вычислительные ресурсы**:
      * Выберите [платформу](../../concepts/vm-platforms.md).
      * Укажите [гарантированную долю](../../../compute/concepts/performance-levels.md) и необходимое количество vCPU, а также объем RAM.
      * При необходимости сделайте виртуальную машину [прерываемой](../../concepts/preemptible-vm.md).
      * (опционально) Включите [программно-ускоренную сеть](../../concepts/software-accelerated-network.md).

  1. В блоке **Сетевые настройки**:

      {% include [network-settings](../../../_includes/compute/network-settings.md) %}

  1. В блоке **Доступ** укажите данные для доступа на виртуальную машину:
      * (опционально) Выберите или создайте [сервисный аккаунт](../../../iam/concepts/users/service-accounts.md). Использование сервисного аккаунта позволяет гибко настраивать права доступа к ресурсам.
      * В поле **Логин** введите имя пользователя.

          {% note alert %}

          Не используйте логин `root` или другие имена, зарезервированные операционной системой. Для выполнения операций, требующих прав суперпользователя, используйте команду `sudo`.

          {% endnote %}

      * В поле **SSH-ключ** вставьте содержимое файла [открытого ключа](../../operations/vm-connect/ssh.md#creating-ssh-keys).
      * Если требуется, разрешите доступ к [серийной консоли](../../operations/serial-console/index.md).

  1. Нажмите кнопку **Создать ВМ**. 
  
  Виртуальная машина появится в списке. При создании виртуальной машине назначаются [IP-адрес](../../../vpc/concepts/address.md) и [имя хоста](../../../vpc/concepts/address.md#fqdn) (FQDN).
  
- CLI
  
  {% include [cli-install](../../../_includes/cli-install.md) %}
  
  {% include [default-catalogue](../../../_includes/default-catalogue.md) %}
  
  1. Посмотрите описание команды CLI для создания виртуальной машины:
  
      ```
      yc compute instance create --help
      ```
  
  1. Получите список дисков в каталоге по умолчанию:
  
      {% include [compute-disk-list](../../../_includes/compute/disk-list.md) %}
  
  1. Выберите идентификатор (`ID`) или имя (`NAME`) нужных дисков.
  1. Создайте виртуальную машину в каталоге по умолчанию:
  
      ```
      yc compute instance create \
        --name first-instance \
        --zone {{ region-id }}-a \
        --network-interface subnet-name=default-a,nat-ip-version=ipv4 \
        --use-boot-disk disk-name=first-disk \
        --attach-disk disk-name=second-disk \
        --ssh-key ~/.ssh/id_rsa.pub
      ```
  
      Данная команда создаст виртуальную машину:
  
      - С именем `first-instance`.

        {% include [name-fqdn](../../../_includes/compute/name-fqdn.md) %}
        
      - В зоне доступности `{{ region-id }}-a`.
      - В подсети `default-a`.
      - С публичным IP и двумя дисками.
 
      {% if product == "cloud-il" %}

      {% include [vm-platform-cli](../../../_includes/compute/vm-platform-cli.md) %}
 
      {% endif %}
  
      Чтобы указать необходимость удаления диска при удалении машины, установите флаг `--auto-delete`:
  
      ```
      yc compute instance create \
        --name first-instance \
        --zone {{ region-id }}-a \
        --network-interface subnet-name=default-a,nat-ip-version=ipv4 \
        --use-boot-disk disk-name=first-disk,auto-delete=yes \
        --attach-disk disk-name=second-disk,auto-delete=yes \
        --ssh-key ~/.ssh/id_rsa.pub
      ```
  
- API
  
  Воспользуйтесь методом [Create](../../api-ref/Instance/create.md) для ресурса `Instance`.

- {{ TF }}

  Если у вас ещё нет {{ TF }}, [установите его и настройте провайдер {{ yandex-cloud }}](../../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).  

  Чтобы создать виртуальную машину из набора дисков:

  1. Опишите в конфигурационном файле параметры ресурсов, которые необходимо создать:

     ```
     resource "yandex_compute_instance" "vm-1" {

       name        = "vm-from-disks"
       platform_id = "standard-v3"

       resources {
         cores  = <количество ядер vCPU>
         memory = <объем RAM в ГБ>
       }

       boot_disk {
         initialize_params {
           disk_id = "<идентификатор загрузочного диска>"
         }
       }

       secondary_disk {
         disk_id = "<идентификатор дополнительного диска>"
       }

       network_interface {
         subnet_id = "${yandex_vpc_subnet.subnet-1.id}"
         nat       = true
       }

       metadata = {
         ssh-keys = "<имя пользователя>:<содержимое SSH-ключа>"
       }
     }

     resource "yandex_vpc_network" "network-1" {
       name = "network1"
     }

     resource "yandex_vpc_subnet" "subnet-1" {
       name       = "subnet1"
       zone       = "<зона доступности>"
       network_id = "${yandex_vpc_network.network-1.id}"
     }
     ```

     Где:

     * `yandex_compute_instance` — описание [виртуальной машины](../../concepts/vm.md):
       * `name` — имя виртуальной машины.
       * `platform_id` — [платформа](../../concepts/vm-platforms.md).
       * `resources` — количество ядер vCPU и объем RAM, доступные виртуальной машине. Значения должны соответствовать выбранной [платформе](../../concepts/vm-platforms.md).
       * `boot_disk` — настройки загрузочного диска. Укажите идентификатор диска. Если у вас нет готового загрузочного диска, укажите [идентификатор публичного образа](../images-with-pre-installed-software/get-list.md) с помощью параметра `image_id`.
       * `secondary_disk` — дополнительный диск для подключения к виртуальной машине. Укажите идентификатор дополнительного диска. Если диска нет, [создайте](../disk-create/empty.md) его.
       * `network_interface` — настройка сети. Укажите идентификатор выбранной подсети. Чтобы автоматически назначить виртуальной машине публичный IP-адрес, укажите `nat = true`.
       * `metadata` — в метаданных необходимо передать открытый ключ для SSH-доступа на виртуальную машину. Подробнее в разделе [{#T}](../../concepts/vm-metadata.md). 
     * `yandex_vpc_network` — описание [облачной сети](../../../vpc/concepts/network.md#network).
     * `yandex_vpc_subnet` — описание [подсети](../../../vpc/concepts/network.md#network), к которой будет подключена виртуальная машина.
            
     {% note info %}

     Если у вас уже есть подходящие ресурсы (облачная сеть и подсеть), описывать их повторно не нужно. Используйте их имена и идентификаторы в соответствующих параметрах.

     {% endnote %}

     Более подробную информацию о ресурсах, которые вы можете создать с помощью {{ TF }}, см. в [документации провайдера]({{ tf-provider-link }}/).

  2. Проверьте корректность конфигурационных файлов.

     1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
     2. Выполните проверку с помощью команды:

        ```
        terraform plan
        ```

     Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, {{ TF }} на них укажет. 

  3. Разверните облачные ресурсы.

     1. Если в конфигурации нет ошибок, выполните команду:

        ```
        terraform apply
        ```

     2. Подтвердите создание ресурсов.

     После этого в указанном каталоге будут созданы все требуемые ресурсы. Проверить появление ресурсов и их настройки можно в [консоли управления]({{ link-console-main }}).

{% endlist %}
