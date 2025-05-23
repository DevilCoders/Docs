# Создание {{ CH }}-кластера

{% if product == "cloud-il" %}

{% include [one-az-disclaimer](../../_includes/overview/one-az-disclaimer.md) %}

{% endif %}

{{ CH }}-кластер — это один или несколько хостов базы данных, между которыми можно настроить репликацию.

{% note info %}

* Количество хостов, которые можно создать вместе с {{ CH }}-кластером, зависит от выбранного {% if audience != "internal" %}[типа хранилища](../concepts/storage.md#storage-type-selection){% else %}[типа хранилища](../concepts/storage.md){% endif %} и [класса хостов](../concepts/instance-types.md#available-flavors).
* Доступные типы хранилища [зависят](../concepts/storage.md) от выбранного [класса хостов](../concepts/instance-types.md#available-flavors).

{% endnote %}

Выбранный [механизм обеспечения работы репликации](../concepts/replication.md) также влияет на количество хостов в кластере из нескольких хостов:

* Кластер, использующий для управления репликацией и отказоустойчивостью {{ CK }}, должен состоять из трех или более хостов — отдельные хосты для запуска {{ CK }} не требуются. Создать такой кластер можно только с помощью CLI и API.

    {% if audience != "internal" %}

    Эта функциональность находится на стадии [Preview](../../overview/concepts/launch-stages.md). Доступ к {{ CK }} предоставляется по запросу. Обратитесь в [техническую поддержку]({{ link-console-support }}) или к вашему аккаунт-менеджеру.

    {% else %}

    Эта функциональность находится на стадии Preview. Доступ к {{ CK }} предоставляется по запросу. Обратитесь в [техническую поддержку]({{ link-console-support }}) или к вашему аккаунт-менеджеру.

    {% endif %}

* При использовании {{ ZK }} кластер может состоять из двух и более хостов. Еще 3 хоста {{ ZK }} будут добавлены в кластер автоматически.

    {% note alert %}

    {% if audience != "internal" %}

    Эти хосты учитываются в расчете использованной [квоты ресурсов]({{ link-console-quotas }}) в облаке и в [расчете стоимости](../pricing.md#prices-zookeeper) кластера.

    {% else %}

    Эти хосты учитываются в расчете использованной [квоты ресурсов]({{ link-console-quotas }}) в облаке.

    {% endif %}

    {% endnote %}

## Как создать кластер {{ CH }} {#create-cluster}

{% list tabs %}

- Консоль управления

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором нужно создать кластер БД.
  {% if audience != "internal" %}
  1. Выберите сервис **{{ mch-name }}**.
  {% endif %}
  1. Нажмите кнопку **Создать кластер**.
  1. Введите имя кластера в поле **Имя кластера**. Имя кластера должно быть уникальным в рамках каталога.
  1. Выберите окружение, в котором нужно создать кластер (после создания кластера окружение изменить невозможно):
      * `PRODUCTION` — для стабильных версий ваших приложений.
      * `PRESTABLE` — для тестирования, в том числе самого сервиса {{ mch-short-name }}. В Prestable-окружении раньше появляются новая функциональность, улучшения и исправления ошибок. При этом не все обновления обеспечивают обратную совместимость.
  1. Выберите версию {{ CH }}, которую будет использовать кластер {{ mch-name }}, из выпадающего списка **Версия**:
     * Для большинства кластеров рекомендуется выбрать самую новую LTS-версию.
     * Для кластеров, в которых планируется использовать гибридное хранилище, рекомендуется выбрать самую новую версию.
  1. Если вы планируете использовать данные из бакета {{ objstorage-name }} с [ограниченным доступом](../../storage/concepts/bucket#bucket-access), то выберите сервисный аккаунт из выпадающего списка или создайте новый. Подробнее о настройке сервисного аккаунта для доступа к данным в бакете см. в разделе [{#T}](s3-access.md).
  1. Выберите класс хостов — он определяет технические характеристики виртуальных машин, на которых будут развернуты хосты БД. Все доступные варианты перечислены в разделе [{#T}](../concepts/instance-types.md). При изменении класса хостов для кластера меняются характеристики всех уже созданных экземпляров.
  1. В блоке **Размер хранилища**:

      {% if audience != "internal" %}

      * Выберите [тип хранилища](../concepts/storage.md).

          {% include [storages-step-settings](../../_includes/mdb/settings-storages.md) %}

      {% endif %}

      * Выберите объем, который будет использоваться для данных и резервных копий. Подробнее о том, как занимают пространство резервные копии, см. раздел [{#T}](../concepts/backup.md).

  1. В блоке **База данных** укажите атрибуты БД:

      * Имя БД.
      * Имя пользователя.
      * Пароль пользователя. Минимум 8 символов.

  1. Пользователями и базами данных кластера можно управлять через SQL.

      {% include [SQL-management-can't-be-switched-off](../../_includes/mdb/mch/note-sql-db-and-users-create-cluster.md) %}

      * Для [управления пользователями через SQL](./cluster-users.md#sql-user-management) включите настройку **Управление пользователями через SQL**.
      * Для [управления базами данных через SQL](./databases.md#sql-database-management) включите настройки **Управление пользователями через SQL** и **Управление базами данных через SQL**.

      При использовании этих настроек укажите пароль пользователя `admin`.

  1. В блоке **Сетевые настройки** выберите облачную сеть для размещения кластера и группы безопасности для сетевого трафика кластера. Может потребоваться дополнительная [настройка групп безопасности](connect.md#configuring-security-groups) для того, чтобы можно было подключаться к кластеру.

  1. В блоке **Хосты** укажите параметры хостов БД, создаваемых вместе с кластером. Чтобы изменить добавленный хост, наведите курсор на строку хоста и нажмите значок ![image](../../_assets/pencil.svg).

  1. При необходимости задайте дополнительные настройки кластера:
     
     {% include [mch-extra-settings](../../_includes/mdb/mch/extra-settings-web-console.md) %}
     
  1. При необходимости задайте [настройки СУБД](../concepts/settings-list.md#dbms-cluster-settings).

  1. Нажмите кнопку **Создать кластер**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы создать кластер:

  {% if audience != "internal" %}

  1. Проверьте, есть ли в каталоге подсети для хостов кластера:

     ```bash
     yc vpc subnet list
     ```

     Если ни одной подсети в каталоге нет, [создайте нужные подсети](../../vpc/operations/subnet-create.md) в сервисе {{ vpc-short-name }}.

  {% endif %}

  1. Посмотрите описание команды CLI для создания кластера:

      ```bash
      {{ yc-mdb-ch }} cluster create --help
      ```

  1. Укажите параметры кластера в команде создания (в примере приведены не все доступные параметры):

     {% if audience != "internal" %}

     ```bash
     {{ yc-mdb-ch }} cluster create \
       --name <имя кластера> \
       --environment <окружение: prestable или production> \
       --network-name <имя сети> \
       --host type=<clickhouse или zookeeper>,zone-id=<зона доступности>,subnet-id=<идентификатор подсети> \
       --clickhouse-resource-preset <класс хоста> \
       --clickhouse-disk-type <network-hdd | network-ssd | local-ssd | network-ssd-nonreplicated> \
       --clickhouse-disk-size <размер хранилища в гигабайтах> \
       --user name=<имя пользователя>,password=<пароль пользователя> \
       --database name=<имя базы данных> \
       --security-group-ids <список идентификаторов групп безопасности> \
       --yandexquery-access=<доступ через {{ yq-full-name }}: true или false> \
       --deletion-protection=<защита от удаления кластера: true или false>
     ```

     Идентификатор подсети `subnet-id` необходимо указывать, если в выбранной зоне доступности создано 2 и больше подсетей.

     {% else %}

      ```bash
      {{ yc-mdb-ch }} cluster create \
        --name <имя кластера> \
        --environment <окружение, prestable или production> \
        --network-id ' ' \
        --host type=<clickhouse или zookeeper>,zone-id=<зона доступности> \
        --clickhouse-resource-preset <класс хоста> \
        --clickhouse-disk-type <local-ssd | local-hdd> \
        --clickhouse-disk-size <размер хранилища в гигабайтах> \
        --user name=<имя пользователя>,password=<пароль пользователя> \
        --database name=<имя базы данных> \
        --security-group-ids <список идентификаторов групп безопасности> \
        --yandexquery-access=<доступ через {{ yq-full-name }}: true или false> \
        --deletion-protection=<защита от удаления кластера: true или false>
      ```

     {% endif %}

     {% include [Ограничения защиты от удаления](../../_includes/mdb/deletion-protection-limits-db.md) %}

     Пользователями и базами данных в кластере можно управлять через SQL.

     {% include [SQL-management-can't-be-switched-off](../../_includes/mdb/mch/note-sql-db-and-users-create-cluster.md) %}

     1. Чтобы включить [режим управления пользователями через SQL](./cluster-users.md#sql-user-management):

         * задайте значение `true` для параметра `--enable-sql-user-management`;
         * задайте пароль для пользователя `admin` в параметре `--admin-password`.

         ```bash
         {{ yc-mdb-ch }} cluster create \
            ...
            --enable-sql-user-management true \
            --admin-password "<пароль пользователя admin>"
         ```

     1. Чтобы включить [режим управления базами данных через SQL](./databases.md#sql-database-management):

         * задайте значение `true` для параметров `--enable-sql-user-management` и `--enable-sql-database-management`;
         * задайте пароль для пользователя `admin` в параметре `--admin-password`.

         ```bash
         {{ yc-mdb-ch }} cluster create \
            ...
            --enable-sql-user-management true \
            --enable-sql-database-management true \
            --admin-password "<пароль пользователя admin>"
         ```

     {% if audience != "internal" and product == "yandex-cloud" %}

     1. Чтобы разрешить доступ к кластеру из сервиса [{{ sf-full-name }}](../../functions/concepts/index.md), передайте параметр `--serverless-access`. Подробнее о настройке доступа см. в документации [{{ sf-name }}](../../functions/operations/database-connection.md).

     {% endif %}

     1. {% include [datatransfer access](../../_includes/mdb/cli/datatransfer-access-create.md) %}

     1. Чтобы включить [{{ CK }}](../concepts/replication.md#ck) в кластере:

        * Задайте версию {{ CH }} (не ниже {{ versions.keeper }}) в параметре `--version`.
        * Задайте значение `true` для параметра `--embedded-keeper`.

         ```bash
         {{ yc-mdb-ch }} cluster create \
            ...
            --version "<версия {{ CH }}: не ниже {{ versions.keeper }}>" \
            --embedded-keeper true
         ```

         {% include [ClickHouse Keeper can't turn off](../../_includes/mdb/mch/note-ck-no-turn-off.md) %}

         Чтобы получить список доступных версий {{ CH }}, выполните команду:

         ```bash
         {{ yc-mdb-ch }} version list
         ```

- {{ TF }}

  {% if audience != "internal" %}
  {% include [terraform-definition](../../_tutorials/terraform-definition.md) %}
  {% endif %}

  Чтобы создать кластер:

    1. В командной строке перейдите в каталог, в котором будут расположены конфигурационные файлы {{ TF }} с планом инфраструктуры. Если такой директории нет — создайте ее.

    {% if audience != "internal" %}
    1. Если у вас еще нет {{ TF }}, [установите его и создайте конфигурационный файл с настройками провайдера](../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).
    
    1. Создайте конфигурационный файл с описанием [облачной сети](../../vpc/concepts/network.md#network) и [подсетей](../../vpc/concepts/network.md#subnet).
        * Сеть — описание [облачной сети](../../vpc/concepts/network.md#network), в которой будет расположен кластер. Если подходящая сеть у вас уже есть, описывать ее повторно не нужно.
        * Подсети — описание [подсетей](../../vpc/concepts/network.md#network), к которым будут подключены хосты кластера. Если подходящие подсети у вас уже есть, описывать их повторно не нужно.

       Пример структуры конфигурационного файла, в котором описывается облачная сеть с одной подсетью:
       
       ```hcl
       resource "yandex_vpc_network" "<имя сети в {{ TF }}>" { name = "<имя сети>" }

       resource "yandex_vpc_subnet" "<имя подсети в {{ TF }}>" {
         name           = "<имя подсети>"
         zone           = "<зона доступности>"
         network_id     = yandex_vpc_network.<имя сети в {{ TF }}>.id
         v4_cidr_blocks = ["<подсеть>"]
       }
       ```
    {% endif %}

    1. Создайте конфигурационный файл с описанием кластера и его хостов.

        * Кластер базы данных — описание кластера и его хостов. Здесь же при необходимости:
            * Задайте [настройки СУБД](../concepts/settings-list.md).
            * Включите защиту от удаления.

                {% include [Deletion protection limits](../../_includes/mdb/deletion-protection-limits-db.md) %}

       Пример структуры конфигурационного файла, в котором описывается кластер из одного хоста:

       ```hcl
       resource "yandex_mdb_clickhouse_cluster" "<имя кластера>" {
         name                = "<имя кластера>"
         environment         = "<окружение>"
         network_id          = yandex_vpc_network.<имя сети в {{ TF }}>.id
         security_group_ids  = ["<список идентификаторов групп безопасности>"]
         deletion_protection = <защита от удаления кластера: true или false>

         clickhouse {
           resources {
             resource_preset_id = "<класс хоста>"
             disk_type_id       = "<тип хранилища>"
             disk_size          = <объем хранилища, ГБ>
           }
         }

         database {
           name = "<имя базы данных>"
         }

         user {
           name     = "<имя пользователя БД>"
           password = "<пароль>"
           permission {
             database_name = "<имя БД, в которой создается пользователь>"
           }
         }

         host {
           type      = "CLICKHOUSE"
           zone      = "<зона доступности>"
           subnet_id = yandex_vpc_subnet.<имя подсети в {{ TF }}>.id
         }
       }
       ```

       {% include [Deletion protection limits](../../_includes/mdb/deletion-protection-limits-db.md) %}

       1. {% include [Maintenance window](../../_includes/mdb/mch/terraform/maintenance-window.md) %}

       1. Чтобы разрешить доступ из других сервисов и [выполнение SQL-запросов из консоли управления](web-sql-query.md), добавьте блок `access` с нужными вам настройками:

           {% if product == "yandex-cloud" %}
          
           ```hcl
           resource "yandex_mdb_clickhouse_cluster" "<имя кластера>" {
             ...
             access {
               datalens   = <Доступ из DataLens: true или false>
               metrika    = <Доступ из Метрики и AppMetrika: true или false>
               serverless = <Доступ из Cloud Functions: true или false>
               web_sql    = <Выполнение SQL-запросов из консоли управления: true или false>
             }
             ...
           }
           ```
 
           {% endif %}
 
           {% if product == "cloud-il" %}
 
           ```hcl
           resource "yandex_mdb_clickhouse_cluster" "<имя кластера>" {
             ...
             access {
               metrika    = <Доступ из Метрики и AppMetrika: true или false>
               web_sql    = <Выполнение SQL-запросов из консоли управления: true или false>
             }
             ...
           }
           ```
          
           {% endif %}
       
       Пользователями и базами данных в кластере можно управлять через SQL.

       {% include notitle [SQL Management can't be switched off](../../_includes/mdb/mch/note-sql-db-and-users-create-cluster.md) %}

       * {% include notitle [Enable SQL user management with Terraform](../../_includes/mdb/mch/terraform/sql-management-users.md) %}

       * {% include notitle [Enable SQL database management with Terraform](../../_includes/mdb/mch/terraform/sql-management-databases.md) %}

       Более подробную информацию о ресурсах, которые вы можете создать с помощью {{ TF }}, см. в [документации провайдера]({{ tf-provider-mch }}).

    1. Проверьте корректность файлов конфигурации {{ TF }}:

       {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Создайте кластер:

       {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

       {% include [explore-resources](../../_includes/mdb/terraform/explore-resources.md) %}

    {% include [Terraform timeouts](../../_includes/mdb/mch/terraform/timeouts.md) %}

- API

  Воспользуйтесь методом API [create](../api-ref/Cluster/create) и передайте в запросе:
  * Идентификатор каталога, в котором должен быть размещен кластер, в параметре `folderId`.
  * Имя кластера в параметре `name`.
  * Окружение кластера в параметре `environment`.
  * Конфигурацию кластера в параметре `configSpec`.
  * Конфигурацию хостов кластера в одном или нескольких параметрах `hostSpecs`.
  * Идентификатор сети в параметре `networkId`.
  * Идентификаторы групп безопасности в параметре `securityGroupIds`.

  При необходимости включите управление пользователями и базами данных через SQL:
  * `configSpec.sqlUserManagement` — задайте значение `true` для включения режима [управления пользователями через SQL](cluster-users.md#sql-user-management).
  * `configSpec.sqlDatabaseManagement` — задайте значение `true` для включения режима [управления базами данных через SQL](databases.md#sql-database-management). Необходимо, чтобы был включен режим управления пользователями через SQL.
  * `configSpec.adminPassword` — задайте пароль пользователя `admin`, с помощью которого осуществляется управление.

  {% include [SQL-management-can't-be-switched-off](../../_includes/mdb/mch/note-sql-db-and-users-create-cluster.md) %}

  {% if audience != "internal" and product == "yandex-cloud" %}
  Чтобы разрешить доступ к кластеру из сервиса [{{ sf-full-name }}](../../functions/concepts/index.md), передайте значение `true` для параметра `configSpec.access.serverless`. Подробнее о настройке доступа см. в документации [{{ sf-name }}](../../functions/operations/database-connection.md).
  {% endif %}

  {% include [datatransfer access](../../_includes/mdb/api/datatransfer-access-create.md) %}

  Чтобы разрешить доступ к кластеру из сервиса {{ yq-full-name }}, передайте значение `true` для параметра `configSpec.access.yandexQuery`.

  При создании кластера из нескольких хостов:

  * Если для параметра `embeddedKeeper` указано значение `true`, для управления репликацией будет использоваться [{{ CK }}](../concepts/replication.md#ck).

      {% include [ClickHouse Keeper can't turn off](../../_includes/mdb/mch/note-ck-no-turn-off.md) %}

      Для использования {{ CK }} необходима версия {{ CH }} не ниже {{ versions.keeper }}. Список доступных версий {{ CH }} можно получить с помощью метода API [list](../api-ref/Versions/list.md).

  * Если значение параметра `embeddedKeeper` не задано или равно `false`, для управления репликацией и распределением запросов будет использоваться {{ ZK }}.

    {% if audience != "internal" %}

    Если в [облачной сети](../../vpc/concepts/network.md) кластера есть подсети в каждой из [зон доступности](../../overview/concepts/geo-scope.md), а настройки хостов {{ ZK }} не заданы, в каждую подсеть будет автоматически добавлено по одному такому хосту.

    Если подсети в сети кластера есть только в некоторых зонах доступности, укажите настройки хостов {{ ZK }} явно.

    {% endif %}

{% endlist %}

{% note warning %}

Если вы указали идентификаторы групп безопасности при создании кластера, то для подключения к нему может потребоваться дополнительная [настройка групп безопасности](connect.md#configuring-security-groups).

{% endnote %}

## Примеры {#examples}

### Создание кластера с одним хостом {#creating-a-single-host-cluster}

{% list tabs %}

- CLI

  Чтобы создать кластер с одним хостом, передайте один параметр `--host`.

  Создайте кластер {{ mch-name }} с тестовыми характеристиками:

  {% if audience != "internal" %}

  * Имя `mych`.
  * Окружение `production`.
  * Сеть `default`.
  * Группа безопасности `{{ security-group }}`.
  * Один хост {{ CH }} класса `{{ host-class }}` в подсети `b0rcctk2rvtr8efcch64`, в зоне доступности `{{ region-id }}-a`.
  * {{ CK }}.
  * Хранилище на сетевых SSD-дисках (`{{ disk-type-example }}`) объемом 20 ГБ.
  * Один пользователь `user1` с паролем `user1user1`.
  * Одна база данных `db1`.
  * Защита от случайного удаления кластера.

  {% else %}

  * Имя `mych`.
  * Окружение `production`.
  * Сеть `default`.
  * Группа безопасности `{{ security-group }}`.
  * Один хост {{ CH }} класса `{{host-class}}` в зоне доступности `{{zone-id}}`.
  * {{ CK }}.
  * Хранилище на локальных SSD-дисках (`local-ssd`) объемом 20 ГБ.
  * Один пользователь `user1` с паролем `user1user1`.
  * Одна база данных `db1`.
  * Защита от случайного удаления кластера.

  {% endif %}

  Выполните следующую команду:

  {% if audience != "internal" %}

  ```bash
  {{ yc-mdb-ch }} cluster create \
    --name mych \
    --environment=production \
    --network-name default \
    --clickhouse-resource-preset {{ host-class }} \
    --host type=clickhouse,zone-id={{ region-id }}-a,subnet-id=b0cl69g98qumiqmtg12a \
    --version {{ versions.keeper }} \
    --embedded-keeper true \
    --clickhouse-disk-size 20 \
    --clickhouse-disk-type {{ disk-type-example }} \
    --user name=user1,password=user1user1 \
    --database name=db1 \
    --security-group-ids {{ security-group }} \
    --deletion-protection=true
  ```

  {% else %}

  ```bash
  {{ yc-mdb-ch }} cluster create \
    --name mych \
    --environment=production \
    --clickhouse-resource-preset s2.nano \
    --host type=clickhouse,zone-id=man \
    --version {{ versions.keeper }} \
    --embedded-keeper true \
    --clickhouse-disk-size 20 \
    --clickhouse-disk-type local-ssd \
    --user name=user1,password=user1user1 \
    --database name=db1 \
    --security-group-ids {{ security-group }} \
    --deletion-protection=true
  ```

{% endif %}

- {{ TF }}

  Создайте кластер {{ mch-name }} и сеть для него с тестовыми характеристиками:

  * Имя `mych`.
  * Окружение `PRESTABLE`.
  * Облако с идентификатором `{{ tf-cloud-id }}`.
  * Каталог с идентификатором `{{ tf-folder-id }}`.
  * Новая облачная сеть `cluster-net`.
  * Новая [группа безопасности по умолчанию](connect.md#configuring-security-groups) `cluster-sg` (в сети `cluster-net`), разрешающая подключение к любому хосту кластера из любой сети (в том числе из интернета) по портам `8443`, `9440`.
  * Один хост класса `{{ host-class }}` в новой подсети `cluster-subnet-{{ region-id }}-a`.
  
    Параметры подсети:
    * диапазон адресов — `172.16.1.0/24`;
    * сеть — `cluster-net`;
    * зона доступности — `{{ region-id }}-a`.

  * Хранилище на {% if audience != "internal" %}сетевых{% else %}локальных{% endif %} SSD-дисках (`{{ disk-type-example }}`) объемом 32 ГБ.
  * Имя базы данных `db1`.
  * Пользователь `user1` с паролем `user1user1`.

  Конфигурационные файлы для такого кластера выглядят так:

  1. Конфигурационный файл с описанием настроек провайдера:

      {% include [terraform-provider](../../_includes/mdb/terraform-provider.md) %}

  1. Конфигурационный файл с описанием облачной сети и подсети:

      {% include [terraform-mdb-single-network](../../_includes/mdb/terraform-single-network.md) %}

  1. Конфигурационный файл с описанием группы безопасности:

      {% include [terraform-mch-sg](../../_includes/mdb/mch/terraform/security-groups.md) %}

  1. Конфигурационный файл с описанием кластера и его хоста:

      {% include [terraform-mch-single-host-single-shard](../../_includes/mdb/mch/terraform/single-host-single-shard.md) %}

{% endlist %}

### Создание кластера из нескольких хостов {#creating-a-multi-host-cluster}

{% list tabs %}

- {{ TF }}

  Создайте кластер {{ mch-name }} с тестовыми характеристиками:

  * Имя `mych`.
  * Окружение `PRESTABLE`.
  * Облако с идентификатором `{{ tf-cloud-id }}`.
  * Каталог с идентификатором `{{ tf-folder-id }}`.
  * Новая облачная сеть `cluster-net`.

  * Три {{ CH }}-хоста класса `{{ host-class }}` и три {{ ZK }}- хоста класса `{{ zk-host-class }}` (для обеспечения работы [репликации](../concepts/replication.md)).

    По одному хосту каждого типа будет размещено в новых подсетях:
    * `cluster-subnet-{{ region-id }}-a`: `172.16.1.0/24`, зона доступности `{{ region-id }}-a`.
    * `cluster-subnet-{{ region-id }}-b`: `172.16.2.0/24`, зона доступности `{{ region-id }}-b`.
    * `cluster-subnet-{{ region-id }}-c`: `172.16.3.0/24`, зона доступности `{{ region-id }}-c`.

    Эти подсети будут принадлежать сети `cluster-net`.

  * Новая [группа безопасности по умолчанию](connect.md#configuring-security-groups) `cluster-sg` (в сети `cluster-net`), разрешающая подключение к любому хосту кластера из любой сети (в том числе из интернета) по портам `8443`, `9440`.
  * Хранилище на {% if audience != "internal" %}сетевых{% else %}локальных{% endif %} SSD-дисках (`{{ disk-type-example }}`) объемом 32 ГБ для каждого {{ CH }}-хоста кластера.
  * Хранилище на {% if audience != "internal" %}сетевых{% else %}локальных{% endif %} SSD-дисках (`{{ disk-type-example }}`) объемом 10 ГБ для каждого {{ ZK }}-хоста кластера.
  * Имя базы данных `db1`.
  * Пользователь `user1` с паролем `user1user1`.

  Конфигурационные файлы для такого кластера выглядят так:

  1. Конфигурационный файл с описанием настроек провайдера:

      {% include [terraform-provider](../../_includes/mdb/terraform-provider.md) %}

  1. Конфигурационный файл с описанием облачной сети и подсетей:

      {% include [terraform-mdb-multiple-networks](../../_includes/mdb/terraform-multiple-networks.md) %}

  1. Конфигурационный файл с описанием группы безопасности:

      {% include [terraform-mch-sg](../../_includes/mdb/mch/terraform/security-groups.md) %}

  1. Конфигурационный файл с описанием кластера и его хостов:

      {% include [terraform-mch-multiple-hosts-single-shard](../../_includes/mdb/mch/terraform/multiple-hosts-single-shard.md) %}

{% endlist %}
