Версия {{newVersion}} отличается в худшую сторону от {{baseVersion}} в категориях:

{% for entity in regresses %}
{{ entity.getName() }}
{% for param in entity.getParams() %}
- {{param}}
{% endfor %}

{% endfor %}

[Ссылка на сравнение](https://pulse.yandex-team.ru/projects/{{projectName}}/new_acceptance?base={{baseVersion}}&channel=Stable&check={{newVersion}})