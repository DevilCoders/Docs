# Уведомления об инцидентах в облаке

По умолчанию информацию об инцидентах в облаке получают его владельцы — все пользователи с ролью `resource-manager.clouds.owner`. 

Чтобы пользователь получал уведомления об инцидентах, следует добавить его в список адресатов уведомлений:

{% list tabs %}

- Консоль управления

  1. Откройте страницу [Уведомления об инцидентах]({{ link-cloud-notifications }}) для выбранного облака.{% if product == "yandex-cloud" %} Если необходимо, [переключитесь на другое облако](switch-cloud.md).{% endif %}
  1. Нажмите кнопку **Добавить**.
  1. Выберите пользователя, которого хотите оповещать об инцидентах и нажмите кнопку **Добавить**.

     {% note info %}

     Добавлять можно пользователей с [аккаунтом {% if product == "yandex-cloud" %}на Яндексе{% endif %}{% if product == "cloud-il" %}Google{% endif %}](../../../iam/concepts/index.md#passport) и [федеративных пользователей](../../../iam/concepts/index.md#saml-federation). Федеративные пользователи должны в собственных настройках учетной записи указать адрес электронной почты.

     {% endnote %}

{% endlist %}
