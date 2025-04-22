**Состав хотфикса**
Функциональные задачи:
{% for issue in issues %}
{{ issue }}
{%- endfor %}

Технические задачи:
{% for issue in techissues %}
{{ issue }}
{%- endfor %}