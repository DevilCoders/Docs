{% extends "telegram/base.md" %}
{% block body %}
😨 Следующие пулл-реквесты не прошли обязательные проверки:
{% for link in pullRequestTelegramLinks %}{{"\n- "}}{{ link }}{% endfor %}

{% for login in authorTgAccounts%}{{login}}{{"\n"}}{% endfor %}

Или какие-то проверки покраснели, или последняя версия изменений не опубликована.
{% endblock body %}