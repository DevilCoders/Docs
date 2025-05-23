{% list tabs %}

- Management console

   1. In the [management console]({{ link-console-main }}), select the folder containing your function.
   1. Open **{{ sf-name }}**.
   1. On the left-hand panel, select ![image](../../_assets/functions/functions.svg) **Functions**.
   1. Select the function to get a list of versions for.
   1. Under **Version history**, you can find the list of function versions and their details.

- CLI

   {% include [cli-install](../cli-install.md) %}

   {% include [default-catalogue](../default-catalogue.md) %}

   To get a list of function versions, run the command:

   ```
   yc serverless function version list --function-name <function name>
   ```

   Result:

   ```
   +----------------------+----------------------+----------+--------------+---------+---------------------+
   |          ID          |     FUNCTION ID      | RUNTIME  |  ENTRYPOINT  |  TAGS   |     CREATED AT      |
   +----------------------+----------------------+----------+--------------+---------+---------------------+
   | b09u830mb1n32a7rj0n8 | b097d9ous3gep99khe83 | python37 | test.handler | $latest | 2019-06-13 09:23:23 |
   | b09ch6pmpohfc9sogj5f | b097d9ous3gep99khe83 | python37 | test.handler | beta    | 2019-06-13 09:12:38 |
   +----------------------+----------------------+----------+--------------+---------+---------------------+
   ```

- API

   You can get a list of function versions using the [listVersions](../../functions/functions/api-ref/Function/listVersions.md) API method.

- Yandex Cloud Toolkit

   You can get a list of versions using the [Yandex Cloud Toolkit plugin]{% if lang == "ru" %}(https://github.com/yandex-cloud/ide-plugin-jetbrains){% endif %}{% if lang == "en" %}(https://github.com/yandex-cloud/ide-plugin-jetbrains/blob/master/README.en.md){% endif %} for the IDE family on the [IntelliJ platform]{% if lang == "ru" %}(https://www.jetbrains.com/ru-ru/opensource/idea/){% endif %}{% if lang == "en" %}(https://www.jetbrains.com/opensource/idea/){% endif %} from [JetBrains](https://www.jetbrains.com/).

{% endlist %}
