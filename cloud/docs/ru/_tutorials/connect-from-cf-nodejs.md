{% note info %}

Руководство предназначено для пользователей Linux. На Windows пройти руководство можно в среде [WSL]{% if lang == "ru" %}(https://docs.microsoft.com/ru-ru/windows/wsl/about){% endif %}{% if lang == "en" %}(https://docs.microsoft.com/en-us/windows/wsl/about){% endif %}.

{% endnote %}

Вы создадите [функцию](../functions/concepts/function.md) с приложением на [Node.js]{% if lang == "ru" %}(https://nodejs.org/ru/){% endif %}{% if lang == "en" %}(https://nodejs.org/en/){% endif %}, которое выполняет простой запрос к базе данных {{ ydb-short-name }}. Развертывание приложения осуществляется с помощью Bash-скриптов, для компиляции используется команда `tcs`.

Функция с привязанным [сервисным аккаунтом](../iam/concepts/users/service-accounts.md) авторизуется в {{ ydb-short-name }} через сервис метаданных.

Приложение создает драйвер подключения к базе {{ ydb-short-name }}, сессию, транзакцию и выполняет запрос, используя библиотеку `ydb`. Эта библиотека устанавливается как [зависимость](../functions/lang/nodejs/dependencies.md) при создании версии функции. Параметры подключения к базе данных передаются в приложение через переменные окружения.

Чтобы настроить подключение к базе данных {{ ydb-short-name }}:

1. [Подготовьте облако к работе](#before-begin).
1. [Подготовьте окружение](#prepare-environment).
1. [Создайте сервисный аккаунт](#create-sa).
1. [Создайте авторизованный ключ](#create-key).
1. [Создайте базу данных {{ ydb-short-name }}](#create-database).
1. [Создайте функцию](#create-function).
1. [Протестируйте функцию](#test-function).

Если созданные ресурсы вам больше не нужны, [удалите их](#clear-out).

## Подготовьте облако к работе {#before-begin}

{% include [before-you-begin](./_tutorials_includes/before-you-begin.md) %}

{% if product == "yandex-cloud" %}

### Необходимые платные ресурсы {#paid-resources}

В стоимость поддержки инфраструктуры для этого сценария входит:

* плата за использование функции (см. [тарифы {{ sf-full-name }}](../functions/pricing.md));
* плата за выполнение запросов к базе данных (см. [тарифы {{ ydb-full-name }}]{% if audience == "external" %}(../ydb/pricing/serverless.md){% else %}(https://cloud.yandex.ru/docs/ydb/pricing/serverless){% endif %}).

{% endif %}

## Подготовьте окружение {#prepare-environment}

1. Клонируйте [репозиторий examples](https://github.com/yandex-cloud/examples/tree/master/serverless/functions/YDB-connect-from-serverless-function) с помощью Git:

   ```
   git clone https://github.com/yandex-cloud/examples.git
   ```

1. В репозитории перейдите в папку с файлами проекта: `examples/tree/master/serverless/functions/YDB-connect-from-serverless-function`.
1. Установите и инициализируйте [интерфейс командной строки {{ yandex-cloud }}](../cli/quickstart.md).
1. Установите утилиту [jq](https://stedolan.github.io/jq/download/). В корне папки с файлами проекта запустите терминал и выполните команду:

   ```bash
   sudo apt-get install jq
   ```

1. Установите [Node.js](https://nodejs.org/en/download/package-manager/), выполнив команду:

   ```
   curl -fsSL https://deb.nodesource.com/setup_current.x | sudo -E bash - \
   sudo apt-get install -y nodejs
   ```

1. Установите зависимости, выполнив команду:

   ```
   npm install
   ```

## Создайте сервисный аккаунт {#create-sa}

{% list tabs %}

- Консоль управления

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором хотите создать сервисный аккаунт.
  1. Выберите вкладку **Сервисные аккаунты**.
  1. Нажмите кнопку **Создать сервисный аккаунт**.
  1. Введите имя сервисного аккаунта: `sa-function`.
  1. Нажмите **Добавить роль** и выберите `editor`.
  1. Нажмите кнопку **Создать**.
 
- CLI

  Выполните команду:

  ```bash
  yc iam service-account create --name sa-function
  ```

  Подробнее о команде `yc iam service-account create` см. в [справочнике CLI](../cli/cli-ref/managed-services/iam/service-account/create.md).

- {{ TF }}

  Если у вас ещё нет {{ TF }}, [установите его и настройте провайдер {{ yandex-cloud }}](../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

  1. Опишите в конфигурационном файле параметры сервисного аккаунта:

     ```
     resource "yandex_iam_service_account" "sa" {
       name = "sa-function"
     }
     ```

     Более подробную информацию о ресурсах, которые вы можете создать с помощью {{ TF }}, см. в [документации провайдера]({{ tf-provider-link }}/iam_service_account).

  1. Проверьте корректность конфигурационных файлов.

     1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
     1. Выполните проверку с помощью команды:

        ```
        terraform plan
        ```

     Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, {{ TF }} на них укажет.

  1. Разверните облачные ресурсы.

     1. Если в конфигурации нет ошибок, выполните команду:

        ```
        terraform apply
        ```

     1. Подтвердите создание ресурсов: введите в терминал слово `yes` и нажмите **Enter**.

- API

  Чтобы создать сервисный аккаунт, воспользуйтесь методом [create](../iam/api-ref/ServiceAccount/create.md) для ресурса [ServiceAccount](../iam/api-ref/ServiceAccount/index.md).

{% endlist %}

## Создайте авторизованный ключ {#create-key}

{% list tabs %}

- Консоль управления

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, которому принадлежит сервисный аккаунт.
  1. Перейдите на вкладку **Сервисные аккаунты**.
  1. Выберите сервисный аккаунт `sa-function` и нажмите на строку с его именем.
  1. Нажмите кнопку **Создать новый ключ** на верхней панели.
  1. Выберите пункт **Создать авторизованный ключ**.
  1. Выберите алгоритм шифрования.
  1. Задайте описание ключа, чтобы потом было проще найти его в консоли управления.
  1. Сохраните открытый и закрытый ключи в файл `service_account_key_file.json`:

     ```json
     {
        "service_account_id": "<идентификатор сервисного аккаунта sa-function>",
        "key_algorithm": "RSA_2048",
        "public_key": "-----BEGIN PUBLIC KEY-----\n...\n-----END PUBLIC KEY-----\n",
        "private_key": "-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
     }
     ```

- CLI

  Выполните команду:

  ```bash
  yc iam key create --service-account-name sa-function -o service_account_key_file.json
  ```

  Подробнее о команде `yc iam key create` см. в [справочнике CLI](../cli/cli-ref/managed-services/iam/key/create.md).

  В случае успеха в файл `service_account_key_file.json` будет записан закрытый ключ (`privateKey`) и идентификатор открытого ключа (`id`).

- {{ TF }}

  1. Опишите в конфигурационном файле параметры ключа:

     ```
     resource "yandex_iam_service_account_key" "sa-auth-key" {
       service_account_id = "<идентификатор сервисного аккаунта sa-function>"
       key_algorithm      = "RSA_2048"
     }
     ```

     Более подробную информацию о ресурсах, которые вы можете создать с помощью {{ TF }}, см. в [документации провайдера]({{ tf-provider-link }}/iam_service_account_key).

  1. Проверьте корректность конфигурационных файлов.

     1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
     1. Выполните проверку с помощью команды:

        ```
        terraform plan
        ```

     Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, {{ TF }} на них укажет.

  1. Разверните облачные ресурсы.

     1. Если в конфигурации нет ошибок, выполните команду:

        ```
        terraform apply
        ```

     1. Подтвердите создание ресурсов: введите в терминал слово `yes` и нажмите **Enter**.

- API

  Чтобы создать ключ доступа, воспользуйтесь методом [create](../iam/api-ref/Key/create.md) для ресурса [Key](../iam/api-ref/Key/index.md).

{% endlist %}

## Создайте базу данных {{ ydb-short-name }} {#create-database}

{% list tabs %}

- Консоль управления

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором хотите создать базу данных.
  1. В списке сервисов выберите **{{ ydb-name }}**.
  1. Нажмите кнопку **Создать базу данных**.
  1. Введите имя базы. Требования к имени:

     {% include [name-format](../_includes/name-format.md) %}

  1. В блоке **Тип базы данных** выберите опцию **Serverless**.
  1. Нажмите кнопку **Создать базу данных**.

     Дождитесь запуска базы данных. В процессе создания база будет иметь статус `Provisioning`. Когда база станет готова к использованию, статус сменится на `Running`.

  1. Нажмите на имя созданной БД.
  1. Сохраните значения полей **Эндпоинт** и **Размещение базы данных** из блока **Соединение**. Они понадобятся на следующем шаге.

{% endlist %}

## Создайте функцию {#create-function}

{% note info %}

Перед созданием функции убедитесь, что в файле `.env` и файлах `create-func.sh` и `create-func-ver.sh` из папки `deploy` в качестве символа перевода строки установлен `LF`.

{% endnote %}

1. Отредактируйте файл `.env`:

   * `ENDPOINT` — строка вида <протокол>://<значение поля **Эндпоинт** из блока **Соединение**>. Например, если протокол `grpcs`, а эндпоинт `ydb.serverless.yandexcloud.net:2135`, введите `grpcs://ydb.serverless.yandexcloud.net:2135`.
   * `DATABASE` — значение поля **Размещение базы данных** из блока **Соединение**.
   * `FUNCTION_NAME` — имя функции: `func-test-ydb`.
   * `FOLDER_ID` — идентификатор каталога.
   * `SERVICE_ACCOUNT_ID` — идентификатор сервисного аккаунта `sa-function`.
   
1. В корне проекта запустите командную строку и выполните команду:

   ```bash
   ./deploy/create-func.sh
   ```

   Этот скрипт создает новую функцию в вашем каталоге и делает ее публичной.

1. Создайте версию функции:

   ```bash
   ./deploy/create-func-ver.sh
   ```

## Протестируйте функцию {#test-function}

{% list tabs %}

- Консоль управления

  1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором находится функция.
  1. В списке сервисов выберите **{{ sf-name }}**.
  1. Выберите функцию `func-test-ydb`.
  1. Перейдите на вкладку **Обзор**.
  1. В блоке **Общая информация** нажмите на ссылку для вызова функции.
  1. В адресной строке браузера добавьте в ссылке параметр `api_key`, например `?api_key=b95`.
  1. При успешном подключении в БД будет создана таблица `b95` и в нее будет добавлена одна запись. На странице появится сообщение в формате JSON, например:

     ```json
     {
        "info": "Создана таблица b95, вставлена одна запись"
     }
     ```

{% endlist %}

## Как удалить созданные ресурсы {#clear-out}

Чтобы перестать платить за созданные ресурсы:

* [удалите базу данных](../ydb/operations/manage-database.md#delete-db);
* [удалите функцию](../functions/operations/function/function-delete.md).
