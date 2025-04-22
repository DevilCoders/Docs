{% extends "telegram/base.md" %}
{% block body %}
В (({{releaseBranchUrl}} релизную ветку)) были успешно влиты следующие пулл-реквесты:
{% for link in pullRequestTelegramLinks %}{{ "\n- " }}{{ link }}{% endfor %}
{% endblock body %}