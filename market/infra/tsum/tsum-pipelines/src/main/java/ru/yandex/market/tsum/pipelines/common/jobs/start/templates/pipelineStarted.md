{% extends "telegram/base.md" %}
{% block body %}
🙏 Пользователем [{{pipelineTriggeredByUserId}}@](https://staff.yandex-team.ru/{{pipelineTriggeredByUserId}}) запущен [релизный пайплайн]({{pipelineURI}}){% endblock body %}