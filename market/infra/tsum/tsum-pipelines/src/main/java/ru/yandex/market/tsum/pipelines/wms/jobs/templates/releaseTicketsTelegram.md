📄 Тикеты в релизе {{fixVersion}}:
{% for issue in issues %}[{{issue.key}}](https://st.yandex-team.ru/{{issue.key}}) {{issue.display.replaceAll("[\\[\\]]", "")}}{% if issue.assignee %} [{{issue.assignee.get(0).login}}@](https://staff.yandex-team.ru/{{issue.assignee.get(0).login}}){% endif %}
{% endfor %}
[Фильтр в трекере]({{releaseFilterUrl}})
