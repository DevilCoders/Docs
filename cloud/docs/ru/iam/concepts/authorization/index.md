# Авторизация в {{ yandex-cloud }}

Когда пользователь выполняет операцию с ресурсом {{ yandex-cloud }}, IAM проверяет, обладает ли пользователь необходимыми разрешениями для этой операции.

Разрешения пользователи получают вместе с ролями на ресурсы. Подробнее о том, как назначаются роли и проверяется список разрешений, читайте в разделе [{#T}](../access-control/index.md).

## Аутентификация в {{ yandex-cloud }} {#authentication}

Перед авторизацией, пользователь должен аутентифицироваться — войти под своим аккаунтом. Аутентификация происходит по-разному в зависимости от типа аккаунта и используемого интерфейса:

* [Аутентификация с аккаунтом {% if product == "yandex-cloud" %}на Яндексе{% endif %}{% if product == "cloud-il" %}Google{% endif %}](#passport)
* [Аутентификация сервисного аккаунта](#sa)
* [Аутентификация федеративного пользователя](#saml-federation)

### Аутентификация с аккаунтом на {{ yandex-cloud }} {#passport}

{% list tabs %}

- Консоль управления

  Аутентификация происходит автоматически, когда вы входите в аккаунт {% if product == "yandex-cloud" %}Яндекса или Яндекс 360{% endif %}{% if product == "cloud-il" %}Google{% endif %}.

{% if audience != "internal" %}

- CLI

  Чтобы выполнять операции в CLI, аутентифицируйтесь по [инструкции](../../../cli/operations/authentication/user.md). После этого аутентификация будет происходить автоматически.

{% endif %}

- API

  {% include [owner-warning](../../../_includes/iam/owner-warning.md) %}

  Чтобы выполнять операции в API:
  
  1. {% if product == "yandex-cloud" %}[Получите IAM-токен](../../operations/iam-token/create.md) в обмен на [OAuth-токен](oauth-token.md).{% endif %}{%if product == "cloud-il" %}[Получите IAM-токен](../../operations/iam-token/create-for-federation.md).{% endif %}
  1. {% include [iam-token-usage](../../../_includes/iam-token-usage.md) %}

     {% include [iam-token-lifetime](../../../_includes/iam-token-lifetime.md) %}

{% endlist %}

### Аутентификация сервисного аккаунта {#sa}

{% list tabs %}

- CLI

  Чтобы выполнять операции в CLI, аутентифицируйтесь по [инструкции](../../../cli/operations/authentication/service-account.md). После этого аутентификация будет происходить автоматически.

- API

  Есть 3 способа выполнять операции от имени сервисного аккаунта:

  * С помощью [IAM-токена](iam-token.md).

      Это рекомендуемый способ аутентификации, но у IAM-токена короткое [время жизни](iam-token.md#lifetime). Поэтому такой способ подойдет для приложений, которые будут запрашивать IAM-токен автоматически.

    {% if product == "yandex-cloud" %}[Инструкция получения IAM-токена](../../operations/iam-token/create-for-sa.md).{% endif %}
  * С помощью [API-ключей](api-key).

      {% include [api-keys-disclaimer](../../../_includes/iam/api-keys-disclaimer.md) %}

      [Инструкция получения API-ключа](../../operations/api-key/create.md).
  * С помощью [статических ключей доступа](access-key.md). Этот способ необходимо использовать в сервисах с AWS-совместимым API, например в {{ objstorage-name }} и {{ message-queue-name }}.

      [Инструкция получения статического ключа доступа](../../operations/sa/create-access-key.md).

{% endlist %}

### Аутентификация федеративного пользователя {#saml-federation}

{% list tabs %}

- Консоль управления

  {% include [federated-user-auth](../../../_includes/iam/federated-user-auth.md) %}

  То, как выглядит процесс аутентификации для федеративного пользователя — зависит от настроек сервера IdP. Подробнее читайте в разделе [{#T}](../../../organization/add-federation.md).

- CLI

  Чтобы выполнять операции в CLI, аутентифицируйтесь по [инструкции](../../../cli/operations/authentication/federated-user.md).

  {% include [include](../../../_includes/cli/success-auth-via-federation.md) %}

{% endlist %}

#### См. также {#see-also}

[{#T}](../index.md#accounts)