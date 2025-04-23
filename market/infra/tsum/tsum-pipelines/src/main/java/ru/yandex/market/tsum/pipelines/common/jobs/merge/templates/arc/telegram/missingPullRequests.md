{% extends "telegram/base.md" %}
{% block body %}
👀 Нет открытых пулл-реквестов в связях тикетов из списка:
{% for link in issueTelegramLinks %}{{"\n- "}}{{ link }}{% endfor %}

{% for login in authorTgAccounts%}{{login}}{{"\n"}}{% endfor %}
{% endblock body %}