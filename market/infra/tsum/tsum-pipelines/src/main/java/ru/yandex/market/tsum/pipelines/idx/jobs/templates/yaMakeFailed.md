**{{context.getJobState().getTitle()}}:** %%ya make%% завершился с ошибками.

Джоба Sandbox создала ресурсы:
{% for resource in resources %}- (({{resource.getHttpLink()}} {{resource.getType()}})): {{resource.getDescription()}}
{% endfor %}
(({{context.getPipeLaunchUrl()}} Перейти к пайплайну))
(({{context.getJobLaunchDetailsUrl()}} Перейти к пайплайн задаче))