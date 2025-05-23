# Создание нового облака

{% if product == "yandex-cloud" %}

[При регистрации](../../../billing/quickstart/index.md#create_billing_account) для вас будет автоматически создано [облако](../../concepts/resources-hierarchy.md#cloud) с именем `cloud-<Яндекс ID>`. После того, как вы привязали платежный аккаунт, вы сможете создать дополнительное облако.

Чтобы создать дополнительное облако:

{% endif %}

{% if product == "cloud-il" %}
{% note info %}

   На стадии [Preview](../../../overview/concepts/launch-stages.md) действует ограничение: доступна только 1 организация и 1 облако.

{% endnote %}

Чтобы создать облако:

{% endif %}

{% list tabs %}

- Консоль управления

  {% if product == "yandex-cloud" %}
  1. [На странице биллинга]({{ link-console-billing }}) убедитесь, что [платежный аккаунт](../../../billing/concepts/billing-account.md) находится в статусе `ACTIVE` или `TRIAL_ACTIVE`. Если платежного аккаунта нет, [создайте его](../../../billing/quickstart/index.md#create_billing_account) или попросите вашего администратора назначить вам роль `billing.accounts.member` на платежный аккаунт.
  {% endif %}
  1. На стартовой странице [консоли управления]({{ link-console-main }}) нажмите значок ![image](../../../_assets/options.svg) напротив своего биллинг-аккаунта.
  1. Выберите **Создать облако**.
  1. Введите имя облака. Требования к имени:

	 {% include [name-format.md](../../../_includes/name-format.md) %}

  1. Укажите организацию, к которой будет привязано облако. Если у вас еще нет организации, она будет создана автоматически.
  1. Нажмите **Создать**. Вы будете перенаправлены на страницу каталога `default` в новом облаке.

- {{ TF }}

  Если у вас ещё нет {{ TF }}, [установите его и настройте провайдер {{ yandex-cloud }}](../../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

  1. Опишите в конфигурационном файле параметры облака, которое необходимо создать:
      * `name` — имя облака. Требования к имени:
      
        {% include [name-format.md](../../../_includes/name-format.md) %}
        
      * `organization_id` — идентификатор организации. {{ TF }} позволяет создать облако только для существующей организации. Перечень идентификаторов организаций можно получить с помощью команды [CLI](../../../cli/quickstart.md): `yc organization-manager organization list`. 

      Пример структуры конфигурационного файла:

      {% if product == "yandex-cloud" %}

      ```hcl
      provider "yandex" {
        token     = "<OAuth>"
        cloud_id  = "<идентификатор облака по умолчанию>"
        folder_id = "<идентификатор каталога по умолчанию>"
        zone      = "<зона доступности по умолчанию>"
      }
     
      resource "yandex_resourcemanager_cloud" "cloud1" {
        name            = "<имя облака>"
        organization_id = "<идентификатор организации>"
      }
      ```

      {% endif %}

      {% if product == "cloud-il" %}

      ```hcl
      provider "yandex" {
        endpoint  = "{{ api-host }}:443"
        token     = "<статический ключ сервисного аккаунта>"
        cloud_id  = "<идентификатор облака по умолчанию>"
        folder_id = "<идентификатор каталога по умолчанию>"
        zone      = "<зона доступности по умолчанию>"
      }
     
      resource "yandex_resourcemanager_cloud" "cloud1" {
        name            = "<имя облака>"
        organization_id = "<идентификатор организации>"
      }
      ```

      {% endif %}

      Более подробную информацию о параметрах ресурса `yandex_resourcemanager_cloud` в {{ TF }}, см. в [документации провайдера]({{ tf-provider-link }}/resourcemanager_cloud).
  1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
  1. Проверьте корректность конфигурационного файла с помощью команды:
      
      ```bash
      terraform validate
      ```
     
      Если конфигурация является корректной, появится сообщение:
     
      ```bash
      Success! The configuration is valid.
      ```

  1. Выполните команду:
      
      ```bash
      terraform plan
      ```
  
      В терминале будет выведен список создаваемых ресурсов и их параметров. На этом этапе изменения не будут внесены. Если в конфигурации есть ошибки, {{ TF }} на них укажет.
  1. Примените изменения конфигурации:

      ```bash
      terraform apply
      ```
     
  1. Подтвердите изменения: введите в терминале слово `yes` и нажмите **Enter**.

      Проверить созданное облако и его параметры можно в [консоли управления]({{ link-console-main }}) или с помощью команды [CLI](../../../cli/quickstart.md):

      ```bash
      yc resource-manager cloud list
      ```

{% endlist %}

{% note info %}

При создании облака вы автоматически получите роль [владельца](../../concepts/resources-hierarchy.md#owner) в этом облаке.

{% endnote %}

#### См. также {#see-also}

* [{#T}](update.md)
* [{#T}](set-access-bindings.md)
* [{#T}](switch-cloud.md)
* [{#T}](../folder/create.md)