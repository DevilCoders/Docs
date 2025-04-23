 # Матрица эскалации NOCDEV

 Матрица эскалации в NOCDEV. 

 В случае возникновения экстренной ситуации процедура эскалации: Контакт 1 --> Контакт 2 --> Менеджер

| Сервис | Контакт 1 | Контакт 2 | Менеджер  |
|--------|:---------:|:---------:|:---------:|
{% for s in service %}
| {{s.name}} | [{{s.contact.chiefdev.name}}]({{s.contact.chiefdev.staff}}) | [{{s.contact.cochiefdev.name}}]({{s.contact.cochiefdev.staff}}) | [{{s.contact.manager.name}}]({{s.contact.manager.staff}}) |
{% endfor %}