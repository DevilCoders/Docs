**Ниже перечислены параметры, которые нужно заполнить после выполнения задачи:**
###
{
{%- for input in inputs %}
  "{{ input }}": ""{{ ", " if not loop.last else "" }}
{%- endfor %}
}
###
Инструкция по параметрам: https://wiki.yandex-team.ru/users/serpentine/new-wh-pipeline/