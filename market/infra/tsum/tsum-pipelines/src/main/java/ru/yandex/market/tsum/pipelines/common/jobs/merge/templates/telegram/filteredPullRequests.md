{% extends "telegram/base.md" %}
{% block body %}
😨 Фильтрация пулл-реквестов в ветку [{{releaseBranch.getName()}}]({{releaseBranch.getHtmlLink()}}) в репозитории [{{repoName}}]({{repoURI}}) отсеяла несколько пулл-реквестов{% endblock body %}