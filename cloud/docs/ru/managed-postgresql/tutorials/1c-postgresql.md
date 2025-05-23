# Создание кластера {{ PG }} для <q>1С:Предприятия</q>

{{ mpg-name }} позволяет создавать отказоустойчивые кластеры {{ PG }}, оптимизированные для работы с системой <q>1С:Предприятие</q>. Для этого в сервисе поддерживаются версии PostgreSQL {{ versions.console.str-1c }}, в которых установлены все необходимые [расширения](#extensions) и изменена конфигурация пулера соединений.

{% note warning %}

Систему <q>1С:Предприятие</q> можно подключить только к кластерам версии {{ versions.console.str-1c }}.

{% endnote %}

При выборе [класса хоста](../concepts/instance-types.md) ориентируйтесь на количество пользователей вашей инсталляции <q>1С:Предприятия</q>. На хостах класса **s2.small** смогут одновременно работать до 50 пользователей. Класс **s2.medium** рекомендуется использовать, если с базой будут работать 50 и более пользователей. Размер хранилища следует выбирать исходя из размеров вашей информационной базы — учитывайте возможный рост объемов данных.

## Создайте кластер {{ mpg-name }} {#create-cluster}

{% list tabs %}

- Вручную

    [Создайте](../operations/cluster-create.md#create-cluster) кластер {{ mpg-name }} любой подходящей конфигурации со следующими настройками:

    * **Имя кластера** — `postgresql-1c`.
    * **Окружение** — `PRODUCTION`.
    * **Версия** — `12-1c`.
    * **Класс хоста** — не ниже `s2.small`.
    * **Размер хранилища** не меньше 10 ГБ.
    * **База данных**:

        * **Имя БД** — `postgresql-1c`.
        * **Имя пользователя** — `user-1c`.
        * **Пароль** — пароль, который вы будете использовать для доступа к кластеру.

    * **Хосты** — добавьте не меньше двух дополнительных хостов, разместив их в разных зонах доступности. Это обеспечит отказоустойчивость кластера. Репликация между хостами будет настроена автоматически. Подробнее см. в разделе [{#T}](../concepts/replication.md).

- С помощью {{ TF }}

    1. Если у вас еще нет {{ TF }}, {% if audience != "internal" %}[установите его](../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform){% else %}установите его{% endif %}.
    1. Скачайте [файл с настройками провайдера](https://github.com/yandex-cloud/examples/tree/master/tutorials/terraform/provider.tf). Поместите его в отдельную рабочую директорию и {% if audience != "internal" %}[укажите значения параметров](../../tutorials/infrastructure-management/terraform-quickstart.md#configure-provider){% else %}укажите значения параметров{% endif %}.
    1. Скачайте в ту же рабочую директорию файл конфигурации кластера [postgresql-1c.tf](https://github.com/yandex-cloud/examples/tree/master/tutorials/terraform/postgresql-1c.tf).

        В этом файле описаны:

        * сеть;
        * подсеть;
        * группа безопасности по умолчанию и правила, необходимые для подключения к кластеру из интернета;
        * кластер {{ mpg-name }} для <q>1С:Предприятия</q>.

    1. Укажите в файле `postgresql-1c.tf` пароль пользователя `user-1c`, который будет использоваться для доступа к кластеру {{ mpg-name }}.
    1. Выполните команду `terraform init` в директории с конфигурационным файлом. Эта команда инициализирует провайдеров, указанных в конфигурационных файлах, и позволяет работать с ресурсами и источниками данных провайдера.
    1. Проверьте корректность файлов конфигурации {{ TF }} с помощью команды:

       ```bash
       terraform validate
       ```

       Если в файлах конфигурации есть ошибки, {{ TF }} на них укажет.

    1. Создайте необходимую инфраструктуру:

       {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

       {% include [explore-resources](../../_includes/mdb/terraform/explore-resources.md) %}

{% endlist %}

Создание кластера БД может занять несколько минут.

## Подключите базу к <q>1С:Предприятию</q> {#connect-to-1c}

Подключите созданную базу в качестве информационной базы <q>1С:Предприятия</q>. При добавлении базы используйте следующие параметры:

* **Защищенное соединение** — отключено.
* **Тип СУБД** — `PostgreSQL`.
* **Сервер баз данных** — `с-<идентификатор кластера>.rw.{{ dns-zone }} port={{ port-mpg }}`.
* **Имя базы данных** — `postgresql-1c`.
* **Пользователь базы данных** — `user-1c`.
* **Пароль пользователя** — `<пароль пользователя базы данных>`.
* **Создать базу данных в случае ее отсутствия** — отключено.

### Расширения {{ PG }} для поддержки системы <q>1С:Предприятие</q> {#extensions}

Список расширений, которые установлены в кластерах PostgreSQL версии {{ versions.console.str-1c }}:

* [online_analyze](https://postgrespro.ru/docs/postgrespro/10/online-analyze)

* [plantuner](https://postgrespro.ru/docs/postgrespro/10/plantuner)

* [fasttrun](https://postgrespro.ru/docs/postgrespro/10/fasttrun)

* [fulleq](https://postgrespro.ru/docs/postgrespro/10/fulleq)

* [mchar](https://postgrespro.ru/docs/postgrespro/10/mchar)

## Удалите созданные ресурсы {#clear-out}

{% list tabs %}

- Вручную

    Если созданные ресурсы вам больше не нужны, [удалите кластер {{ mpg-name }}](../operations/cluster-delete.md).

- С помощью {{ TF }}

    Чтобы удалить инфраструктуру, [созданную с помощью {{ TF }}](#create-cluster):

    1. В терминале перейдите в директорию с планом инфраструктуры.
    1. Удалите файл `postgresql-1c.tf`.
    1. Проверьте корректность файлов конфигурации {{ TF }} с помощью команды:

        ```bash
        terraform validate
        ```

        Если в файлах конфигурации есть ошибки, {{ TF }} на них укажет.

    1. Подтвердите изменение ресурсов.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

        Все ресурсы, которые были описаны в файле `postgresql-1c.tf`, будут удалены.

{% endlist %}
