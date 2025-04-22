{% extends "telegram/base.md" %}
{% block body %}
🤙 Успешно смержены фича-ветки в ветку [{{releaseBranch.getName()}}]({{releaseBranch.getHtmlLink()}}) в репозитории [{{repoName}}]({{repoURI}}){% endblock body %}