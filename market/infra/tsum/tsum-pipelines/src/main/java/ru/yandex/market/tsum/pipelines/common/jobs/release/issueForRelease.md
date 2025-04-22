{% block body %}📄 Следующие тикеты выбраны для релиза {{version}}:
{% for issue in issues %}[{{issue.key}} {{issue.display.replaceAll("[\\[\\]]", "")}}](https://st.yandex-team.ru/{{issue.key}}){% if issue.assignee %} [{{issue.assignee.get(0).login}}@](https://staff.yandex-team.ru/{{issue.assignee.get(0).login}}){% endif %}
{% endfor %}{% endblock body %}