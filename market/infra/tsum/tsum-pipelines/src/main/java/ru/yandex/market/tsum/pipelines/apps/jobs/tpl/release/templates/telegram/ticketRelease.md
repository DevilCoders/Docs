{% block body %}
🚀 Тикет попал в релиз
[{{issue.getKey()}}](https://st.yandex-team.ru/{{issue.getKey()}}) {{issue.getSummary()}}
{% for tag in issue.getTags() %}{{ " #" }}{{ tag }}{% endfor %}
{% endblock body %}
{% block footer %}Релиз [{{fixVersion.getName()}}]({{releaseFilterUrl}}), релизный тикет [{{releaseIssue}}](https://st.yandex-team.ru/{{releaseIssue}}){% endblock %}