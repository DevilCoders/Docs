🛠️ *Пайплайн {{pipeId}} мёржит бранч `{{sourceBranch}}` в `{{targetBranch}}`*


{%- if (releaseInfo != null) %}
Релиз: `{{releaseInfo.getFixVersion().getName()}}`, [Тикет в Startrek](https://st.yandex-team.ru/{{releaseInfo.getReleaseIssueKey()}})
{%- endif %}
{%- if printHashBeforeMerge %}
Хэш до мерджа: {{baseHash}} 
{%- endif %}

[Пулл реквест]({{prUrl}})
[Перейти к пайплайну]({{context.getPipeLaunchUrl()}})
[Перейти к пайплайн задаче]({{context.getJobLaunchDetailsUrl()}})

#{{pipeId}} #{{targetBranch.replaceAll("[_-]", "")}} {{customTags}}
--------
