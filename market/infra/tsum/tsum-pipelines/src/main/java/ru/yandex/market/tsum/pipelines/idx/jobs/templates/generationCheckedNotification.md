**{{context.getJobState().getTitle()}}:** завершена раскладка поколения с версией индексатора {{releaseVersion}}.

Статус поколения — **{{result.getStatus()}}**.

{% if !result.getChecks().isEmpty() %}Результаты проверок под репортом:
{% for kv in result.getChecks().entrySet() %}- {% if !kv.getValue() %}!!{% endif %}{{kv.getKey()}} — {% if !kv.getValue() %}не {% endif %}прошла{% if !kv.getValue() %}!!{% endif %}
{% endfor %}{% endif %}
(({{context.getPipeLaunchUrl()}} Перейти к пайплайну))
(({{context.getJobLaunchDetailsUrl()}} Перейти к пайплайн задаче))