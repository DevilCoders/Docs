{%- if (releaseInfo != null) %}Релизный тикет: [{{releaseInfo.getReleaseIssueKey()}}]({{releaseInfo.getReleaseIssueUrl()}}).
В релизе {{releaseInfo.getFixVersion().getName()}} тикеты:
{% else %}К проверке готовы тикеты:
{% endif %}
{% for QA, issueLinksList in qaTicketLists.items() %}{{ QA }}
{% for link in issueLinksList %}link
{% endfor %}
{% endfor %}
Напишите, нужен ли вам ран?
