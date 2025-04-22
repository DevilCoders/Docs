🚗 Релиз [{{releaseName}}]({{releaseFilterUrl}}) выложен в БТ, релизный тикет [{{releaseTicketKey}}]({{releaseIssueUrl}})

{%- if (testScopedIssues.isEmpty()) %}

Релиз не содержит тикетов, требующих ручного тестирования
{%- else %}

*Тикеты, требующие ручного тестирования:*
{% for issue in testScopedIssues -%}
[{{issue.getIssueKey()}}]({{issue.getIssueURL()}}){%- if issue.isAlreadyTested() %} — повторный тест.{%- endif %} ```* {{issue.getIssueTitle()}} {{issue.getAssigneeName()}}``` {{issue.getAssigneeTelegramLogin()|replace("_", "\\_")}}
{% endfor %}
{%- endif %}

{%- if (!taggedForNotificationIssues.isEmpty()) %}

*Тикеты c тегами уведомлений:*
{% for issue in taggedForNotificationIssues -%}
[{{issue.getIssueKey()}}]({{issue.getIssueURL()}}) — {{issue.getAssigneeTelegramLogin()|replace("_", "\\_")}}
{% endfor %}
{%- endif %}
Для уведомления о деплое добавьте в тикет тег `notify_deploy`.