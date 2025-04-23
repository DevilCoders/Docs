{% extends "telegram/base.md" %}
{% block body %}
😱 При попытке слияния изменений в ветку [{{releaseBranch.getName()}}]({{releaseBranch.getHtmlLink()}}) в репозитории [{{repoName}}]({{repoURI}}) произошёл конфликт{% endblock body %}