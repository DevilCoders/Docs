{% for status_name, counter in status_counter.items() %}
    {%- if counter.increase or counter.decrease -%}
        !!({{ status_color_map[status_name] }})**{{ status_name }}**!!: {{ counter.count }}
        {%- if counter.increase -%}
            ({%- if text_report_links[status_name] -%}
                (({{ text_report_links[status_name]}} +{{ counter.increase }}))
            {%- else -%}
                +{{ counter.increase }}
            {%- endif -%})
        {%- endif -%}
        {%- if counter.decrease -%}
            (-{{ counter.decrease }})
        {%- endif %}
{% else -%}
    {%- endif -%}
{% endfor -%}
