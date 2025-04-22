Тикет создан автоматически с помощью релизного пайплайна.
Ссылка на пайплайн: {{context.getPipeLaunchUrl()}}
Ссылка на задачу: {{context.getJobLaunchDetailsUrl()}}

{%- if (releaseInfo != null) %}

Релиз: {{releaseInfo.getFixVersion().getName()}}
Тикет: https://st.yandex-team.ru/{{releaseInfo.getReleaseIssueKey()}}

{%- endif %}


{%- if (!changelog.isEmpty()) %}

Изменения:
{{changelog}}
{%- endif %}


Pipe job id: {{context.getFullJobId()}}
Pipeline id: {{context.getPipeLaunch().getPipeId()}}