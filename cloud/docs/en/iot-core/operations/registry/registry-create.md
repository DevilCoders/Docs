# Creating a registry

{% list tabs %}

- Management console

   To create a registry:

   1. In the [management console]({{ link-console-main }}), select the folder where you wish to create your registry.
   1. Select **{{ iot-short-name }}**.
   1. Click **Create registry**.
   1. Under **General information**, add:
      - A **name** for the registry. For example, `my-registry`.
      - (optional) A **description** with further information about the registry.
      - A **password** that you will be using for registry access.<br/>You can use a [password generator](https://passwordsgenerator.net/) to create one.<br/>Make sure to save the password — you will need it later.
      - (optional) To assign a label to the registry, fill in the **Key** and **Value** fields and click **Add label**.
   1. (optional) Add [certificates](../../operations/certificates/create-certificates.md):
      - To add a file:
         1. Choose the **File** method.
         1. Click **Select file**.
         1. Specify the certificate file on your computer and click **Open**.
         1. Click **Add**.
      - To add text:
         1. Choose the **Text** method.
         1. Insert the certificate body in the **Contents** field.
         1. Click **Add**.
   1. Click **Create**.

- CLI

   {% include [cli-install](../../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../../_includes/default-catalogue.md) %}

   1. Create a registry:

      ```
      yc iot registry create --name my-registry
      ```

      {% include [name-format](../../../_includes/name-format.md) %}

      Result:
      ```
      id: b91ki3851hab9m0l68je
      folder_id: aoek49ghmknnpj1ll45e
      created_at: "2019-05-28T11:29:42.420Z"
      name: my-registry
      ```

   1. Make sure the registry was created:

      ```
      yc iot registry list
      ```

      Result:
      ```
      +----------------------+-------------+
      |          ID          |    NAME     |
      +----------------------+-------------+
      | b91ki3851hab9m0l68je | my-registry |
      +----------------------+-------------+
      ```

- {{ TF }}

   {% include [terraform-definition](../../../_tutorials/terraform-definition.md) %}

   If you don't have {{ TF }}, [install it and configure the {{ yandex-cloud }} provider](../../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

   {% note info %}

   To add certificates to a registry, [generate](../certificates/create-certificates.md) them in advance.

   {% endnote %}

   To create a device registry:

   1. In the configuration file, describe the parameters of the resource to create:

      * `yandex_iot_core_registry`: Registry parameters:
        * `name`: Registry name.
        * `description`: Registry description.
        * `labels`: Registry labels in `key:value` format.
        * `passwords`: List of registry passwords for authorization using a [username and password](../../concepts/authorization.md#log-pass).
        * `certificates`: List of registry certificates for authorization using [certificates](../../concepts/authorization.md#certs).

      Example configuration file structure:

      ```
      resource "yandex_iot_core_registry" "my_registry" {
        name        = "test-registry"
        description = "test registry for terraform provider documentation"
        labels = {
          test-label = "label-test"
        }
      
        passwords = [
          "<password 1>",
          "<password 2>"
        ]
      
        certificates = [
          file("<path to first certificate file>"),
          file("<path to second certificate file>")
        ]
      }
      
      output "yandex_iot_core_registry_my_registry" {
        value = "${yandex_iot_core_registry.my_registry.id}"
      }
      ```

      For more information about the resources you can create using {{ TF }}, see the [provider documentation]({{ tf-provider-link }}).

   2. Make sure that the configuration files are correct.

      1. In the command line, go to the directory where you created the configuration file.
      2. Run the check using the command:
         ```
         terraform plan
         ```
      If the configuration is described correctly, the terminal displays a list of created resources and their parameters. If there are errors in the configuration, {{ TF }} points them out.

   3. Deploy the cloud resources.

      1. If the configuration doesn't contain any errors, run the command:
         ```
         terraform apply
         ```
      2. Confirm that you want to create the resources.

      Afterwards, all the necessary resources are created in the specified folder. You can check that the resources are there with the correct settings using the [management console]({{ link-console-main }}).

{% endlist %}
