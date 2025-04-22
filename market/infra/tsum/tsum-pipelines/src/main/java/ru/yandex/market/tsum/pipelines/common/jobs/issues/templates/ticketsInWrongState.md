Тикеты в некорректном статусе:
{% for issue in issuesInWrongStatus-%}
[{{issue.getKey()}}]({{issue.getSelf().toString()}}) ```{{issue.getSummary()}}}``` {{issue.getStatus().getKey()}}
{% endfor %}
Необходим один из статусов: {{allowedStatuses}}