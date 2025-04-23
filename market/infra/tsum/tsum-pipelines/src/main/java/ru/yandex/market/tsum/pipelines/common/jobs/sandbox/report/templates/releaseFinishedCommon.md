🛠️ Пайплайн {{pipeId}}: Рестарт на версию {{fixVersion}} в {{releaseType}} закончен. На этой версии работает {{updatedHostRatio}} хостов:

Пайплайн: {{context.getPipeLaunch().getPipeId()}}, релиз: {{releaseInfo.getFixVersion().getName()}}
Тикет в Startrek: https://st.yandex-team.ru/{{releaseInfo.getReleaseIssueKey()}}


Перейти к пайплайну: {{context.getPipeLaunchUrl()}}
Перейти к пайплайн задаче: {{context.getJobLaunchDetailsUrl()}}
--------
#release
