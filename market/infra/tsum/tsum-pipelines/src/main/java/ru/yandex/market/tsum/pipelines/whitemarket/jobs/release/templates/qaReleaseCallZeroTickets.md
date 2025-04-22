{%- if (releaseInfo != null) %}Релизный тикет: [{{releaseInfo.getReleaseIssueKey()}}]({{releaseInfo.getReleaseIssueUrl()}}).
В релизе {{releaseInfo.getFixVersion().getName()}} нет тикетов для проверки.
{% else %}Нет тикетов, готовых к проверке.
{% endif %}
