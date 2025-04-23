{% if failedSlas.size() > 1 %}
Следующие SLA были нарушены:
{% for sla in failedSlas %}
{{sla.caseName}} {{sla.percentile}} <{{sla.timingMs}}
{% endfor %}
