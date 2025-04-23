**{{context.getJobState().getTitle()}}:** завершены проверки в Juggler:

{% for event in events %}- !!({{helper.getColor(event)}})**{{event.getService()}}** ({{event.getHost()}} @ {{helper.getDate(event)}})!!
{% endfor %}
(({{context.getPipeLaunchUrl()}} Перейти к пайплайну))
(({{context.getJobLaunchDetailsUrl()}} Перейти к пайплайн задаче))