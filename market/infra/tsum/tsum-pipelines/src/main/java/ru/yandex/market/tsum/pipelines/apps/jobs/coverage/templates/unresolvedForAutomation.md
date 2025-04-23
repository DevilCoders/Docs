Завершите работы по задачам автоматизации:
{% for issue in issues %}{{issue.key}}
{% endfor %}

Ссылка на пайплайн: {{pipeLaunchUrl}}
Ссылка на джобу: {{jobLaunchUrl}}