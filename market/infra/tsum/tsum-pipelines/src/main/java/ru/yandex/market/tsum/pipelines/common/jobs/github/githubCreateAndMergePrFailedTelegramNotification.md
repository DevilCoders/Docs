🛠️ *Пайплайну {{pipeId}} не удалось смёржить бранч `{{sourceBranch}}` в `{{targetBranch}}`*


{%- if (releaseInfo != null) %}
Релиз: `{{releaseInfo.getFixVersion().getName()}}`, [Тикет в Startrek](https://st.yandex-team.ru/{{releaseInfo.getReleaseIssueKey()}})
{%- endif %}

[Пулл реквест]({{prUrl}})
[Перейти к пайплайну]({{context.getPipeLaunchUrl()}})
[Перейти к пайплайн задаче]({{context.getJobLaunchDetailsUrl()}})

#{{pipeId}} #{{targetBranch.replaceAll("[_-]", "")}}
--------
