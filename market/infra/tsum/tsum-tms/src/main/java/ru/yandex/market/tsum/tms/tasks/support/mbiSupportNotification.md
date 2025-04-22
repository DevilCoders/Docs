{% if recentCount == 0 %}
Сегодня неразобранных тикетов нет.
{% else %}
Сегодня создано {{recentCount}} тикетов {% if recentCount > 10 %}. Первые {{recentIssues.size()}} по весу{% endif %}:
{% for issue in recentIssues.toList() %}
[{{issue.getKey()}}](https://st.yandex-team.ru/{{issue.getKey()}}) {{issue.getDisplay()}}
{% endfor %}{% endif %}
[Всего неразобранных тикетов]({{filterUrl}}): {{totalCount}}.