📄 Тикеты в релизе {{fixVersion}}:
{% for issue in issues %}{{issue.key}} {{issue.display}}{% if issue.assignee %} {{issue.assignee.get(0).login}}@{% endif %}
{% endfor %}
Фильтр в трекере: ({{releaseFilterUrl}})
Фильтр в трекере на тикеты с ручным тестированием: {{releaseFilterWithManualTestingUrl}}