# Удалить снимок диска

{% note warning %}

Удаление снимка — неотменяемая и необратимая операция, восстановить удаленный снимок невозможно.

{% endnote %}

Чтобы удалить снимок:

{% list tabs %}

- Консоль управления
  
  1. В консоли управления выберите каталог, которому принадлежит снимок.
  1. Выберите сервис **{{ compute-name }}**.
  1. На панели слева выберите ![image](../../../_assets/compute/snapshots.svg) **Снимки дисков**.
  1. В строке с нужным снимком нажмите значок ![image](../../../_assets/dots.svg) и выберите в меню команду **Удалить**.
  1. Подтвердите удаление.
  
- CLI
  
  {% include [default-catalogue](../../../_includes/default-catalogue.md) %}
  
  1. Посмотрите описание команд CLI для удаления снимков:
  
      ```
      yc compute snapshot delete --help
      ```
  
  1. Получите список снимков в каталоге по умолчанию:
  
      {% include [compute-snapshot-list](../../_includes_service/compute-snapshot-list.md) %}
  
  1. Выберите идентификатор (`ID`) или имя (`NAME`) нужного снимка.
  1. Удалите снимок:
  
      ```
      yc compute snapshot delete \
        --name first-snapshot
      ```

- {{ TF }}

  Подробнее о {{ TF }} [читайте в документации](../../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

  Если вы создавали снимок диска с помощью {{ TF }}, вы можете удалить его:

  1. В командной строке перейдите в папку, где расположен конфигурационный файл {{ TF }}.
  2. Удалите ресурсы с помощью команды:

      ```
      terraform destroy
      ```

      {% note alert %}

      {{ TF }} удалит все ресурсы, созданные в текущей конфигурации: кластеры, сети, подсети, виртуальные машины и т. д.

      {% endnote %}

  3. Подтвердите удаление ресурсов.

{% endlist %}
