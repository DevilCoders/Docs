🛠️ *Кондукторный тикет в {{branch.toLowerCase()}} завис*
Пайплайн *{{pipeId}}*

Тикет деплоится больше {{timeoutMinutes}} минут.

Пакеты:
{% for package in packages %}{{ package.getDebianId() }}
{% endfor %}

{%- if (releaseInfo != null) %}
Релиз: {{releaseInfo.getFixVersion().getName()}}, [Тикет в Startrek](https://st.yandex-team.ru/{{releaseInfo.getReleaseIssueKey()}})
{%- endif %}

[Тикет в Conductor]({{ticketUrl}})
[Перейти к пайплайну]({{context.getPipeLaunchUrl()}})
[Перейти к пайплайн задаче]({{context.getJobLaunchDetailsUrl()}})

#{{pipeId}} #{{branch.toLowerCase()}}
--------
