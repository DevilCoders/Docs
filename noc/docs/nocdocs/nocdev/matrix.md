# Матрица эскалации систем NOCDEV

## Критичные системы

В таблице ниже приведен список систем критичных для работы Yandex. В случае возникновения экстренной ситуации процедура эскалации: Контакт 1 --> Контакт 2 --> Менеджер

| Сервис | Контакт 1 | Контакт 2 | Менеджер  |
|--------|:---------:|:---------:|:---------:|
{% for s in service %}
{% if s.missioncritical %}
| {{s.name}} | [{{s.contact.chiefdev.name}}]({{s.contact.chiefdev.staff}}) | [{{s.contact.cochiefdev.name}}]({{s.contact.cochiefdev.staff}}) | [{{s.contact.manager.name}}]({{s.contact.manager.staff}}) |
{% endif %}
{% endfor %}

## Полный список систем

Полный список систем:

{% cut "Полный список систем..." %}

| Сервис | Контакт 1 | Контакт 2 | Менеджер  |
|--------|:---------:|:---------:|:---------:|
{% for s in service %}
| {{s.name}} | [{{s.contact.chiefdev.name}}]({{s.contact.chiefdev.staff}}) | [{{s.contact.cochiefdev.name}}]({{s.contact.cochiefdev.staff}}) | [{{s.contact.manager.name}}]({{s.contact.manager.staff}}) |
{% endfor %}

{% endcut %}