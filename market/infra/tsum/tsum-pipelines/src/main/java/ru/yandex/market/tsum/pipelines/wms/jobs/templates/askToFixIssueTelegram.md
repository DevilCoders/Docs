Пожалуйста, заполните поле "Manual Testing" и переведите в статус "Ready for Prestable" следующие задачи:
{% for contact in contacts -%}
@{{ contact.telegram }}
{% for issue in contact.issues -%}
https://st.yandex-team.ru/{{ issue }}
{% endfor %}
{% endfor %}