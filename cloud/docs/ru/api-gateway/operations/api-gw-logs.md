---
title: "Просмотр журнала выполнения в {{ api-gw-full-name }}"
description: "Вы можете Просмотр журнала выполнения в {{ api-gw-full-name }} с помощью консоли управления. Для этого выберите сервис {{ api-gw-name }}, выберите API-шлюз, журнал выполнения которого вы хотите посмотреть. В открывшемся окне перейдите в раздел Логи и укажите период. По умолчанию задан период за 1 час. Время в журнале выполнения указано по UTC."
---

# Просмотр журнала выполнения

Время в журнале выполнения указано по [UTC]{% if lang == "ru" %}(https://ru.wikipedia.org/wiki/Всемирное_координированное_время){% endif %}{% if lang == "en" %}(https://en.wikipedia.org/wiki/Coordinated_Universal_Time){% endif %}.

{% list tabs %}

- Консоль управления

    1. В [консоли управления]({{ link-console-main }}) выберите сервис **{{ api-gw-name }}**.
    1. Выберите API-шлюз, журнал выполнения которого вы хотите посмотреть.
    1. В открывшемся окне перейдите в раздел **Логи** и укажите период. По умолчанию задан период за 1 час.

{% endlist %}

Подробнее о работе с логами в [документации {{ cloud-logging-full-name }}](../../logging/).
