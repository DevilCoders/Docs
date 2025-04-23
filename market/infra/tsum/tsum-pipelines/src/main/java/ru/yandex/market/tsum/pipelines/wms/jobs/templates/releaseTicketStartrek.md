**Состав релиза**

Функциональные задачи:
{% for issue in func %}
{{ issue }}
{%- endfor %}

Технические задачи:
{% for issue in tech %}
{{ issue }}
{%- endfor %}

Не определено:
{% for issue in unsorted %}
{{ issue }}
{%- endfor %}

**Выложено в прод:**