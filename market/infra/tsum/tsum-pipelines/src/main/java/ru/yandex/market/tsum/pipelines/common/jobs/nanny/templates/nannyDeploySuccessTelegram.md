🛠️ *Пайплайн {{pipeId}} успешно выложил через Nanny в {{environment.toLowerCase()}}*
{%- if (releaseInfo != null) %}
Релиз: *{{releaseInfo.getFixVersion().getName()}}*, [Тикет в Startrek](https://st.yandex-team.ru/{{releaseInfo.getReleaseIssueKey()}})
{% endif %}

{%- if (recipeId != null) %}
Рецепт: *{{recipeId}}*
{%- endif %}
{%- if (dashboardId != null) %}
Дашборд: *{{dashboardId}}*
{% endif %}

{%- if (sandboxResourceTypes != null && !sandboxResourceTypes.isEmpty()) %}
Sandbox ресурсы:
{%- for sandboxResource in sandboxResourceTypes %}
*{{ sandboxResource }}*
{%- endfor %}
{% endif %}

{%- if (!sandboxUrls.isEmpty()) %}
Ссылки в Sandbox:
{%- for sandboxUrl in sandboxUrls %}
[{{ sandboxUrl }}]
{%- endfor %}
{% endif %}

{%- if (!nannyUrls.isEmpty()) %}
Ссылки в Nanny:
{%- for nannyUrl in nannyUrls %}
[{{ nannyUrl }}]
{%- endfor %}
{% endif %}

{%- if (!changelog.isEmpty()) %}
*Изменения:*
```
{{changelog}}
```
{%- endif -%}

[Перейти к пайплайну]({{context.getPipeLaunchUrl()}})
[Перейти к пайплайн задаче]({{context.getJobLaunchDetailsUrl()}})

#{{pipeId}} #{{environment.toLowerCase()}}
--------
