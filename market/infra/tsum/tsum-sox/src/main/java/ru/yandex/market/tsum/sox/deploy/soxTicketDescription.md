В релизе в окружения {{taskParameters.getEnvironments()}} через задачу в {{taskParameters.getTaskType().getTypeName()}} {{taskParameters.getTaskKey()}} ({{taskParameters.getTaskLink()}}) не соблюдена процедура выкладки SOX ресурсов.

Обнаруженные проблемы (для прохождения валидации достаточно одного ST тикета удовлетворяющего всем условиям):
{% for problem in problems -%}
* {{problem}}
{% endfor %}
Выкладываемые ресурсы:
{% for resource in taskParameters.getResourcesInTask() -%}
* {{resource.getResourceName()}}{{'\t'}}{{resource.getResourceVersion()}}
{%- if resource.isSox() %} (Под Sox)
{%- else %} (Не Sox)
{%- endif %}
{% endfor %}
Подробности о процессе: https://wiki.yandex-team.ru/Market/releases/release-ticket/#sobljudenietrebovanijjsox
