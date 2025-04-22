**Требуется подтверждение релиза**

Для его подтверждения или отклонения, необходимо закрыть тикет и выставить нужную резолюцию.
Список резолюций:
**Отказ** - отклонить данный релиз.
**Реакция не нужна** - данный релиз будет одобрен и для данной версии пайплайна больше не будет требоваться подтверждение релиза, подтверждение потребуется при активации новой версии пайплайна.
**До следующего обращения** - данный релиз будет одобрен, новый созданный релиз потребует подтверждения. 

Проект: [{{jobContext.getProjectId()}}]({{tsumUrl}}pipe/projects/{{jobContext.getProjectId()}})
Пайплайн: [{{jobContext.getPipeLaunch().getPipeId()}}]({{tsumUrl}}pipe/projects/{{jobContext.getProjectId()}}/pipelines/{{jobContext.getPipeLaunch().getPipeId()}})
Версия пайплайна: [{{jobContext.getPipeLaunch().getPipelineVersion()}}]({{tsumUrl}}pipe/projects/{{jobContext.getProjectId()}}/pipelines/{{jobContext.getPipeLaunch().getPipeId()}}/diff/{{jobContext.getPipeLaunch().getPipelineVersion()}})

{%- if (releaseInfo != null) %}
Релиз: {{releaseInfo.getFixVersion().getName()}},
[Релизный тикет]({{releaseInfo.getReleaseIssueUrl().toString()}})
{%- endif %}

[Ссылка на релизный пайплайн]({{jobContext.getPipeLaunchUrl()}}) 

[Документация]({{wikiUrl}})