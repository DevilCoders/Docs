{% extends "telegram/base.md" %}
{% block body %}
😱 Следующие тикеты конфликтуют или с транком, или с тикетами этого релиза:
{% for link in pullRequestTelegramLinks %}{{"\n- "}}{{ link }}{% endfor %}

{% for login in authorTgAccounts%}{{login}}{{"\n"}}{% endfor %}

Ребейзните свой PR на свежий транк.
Если конфликтов не будет - то ребейзните ещё раз после завершения этого релиза.
{% endblock body %}