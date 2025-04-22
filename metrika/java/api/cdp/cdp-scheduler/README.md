# CDP-SCHEDULER
Сервис исполняющий периодические (cron) задачи для нужд CDP.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-scheduler` - сервис, исполняющий периодические (cron) задачи для нужд CDP. Технический каждый инстанс `cdp-scheduler`
является bazinga worker-ом, с предопределённым набором тасок, которые он умеет выполнять. К сожалению, вменяемого описания
для bazinga не существует.


### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-scheduler-production

testing - https://deploy.yandex-team.ru/stages/cdp-scheduler-test

### Что делает?
Для ответа на этот вопрос стоит обратиться к описаниям каждой конкретной задачи. Все задачи являются наследниками
[LoggingTask](https://a.yandex-team.ru/arc_vcs/metrika/java/api/bazinga-common/src/java/ru/yandex/metrika/task/LoggingTask.java) и
располагаются в [папке src/java/ru/yandex/metrika/cdp/scheduler/tasks](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-scheduler/src/java/ru/yandex/metrika/cdp/scheduler/tasks/).
Конфиги запусков тасок находятся в [файле cdp-scheduler-tasks.xml](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-scheduler/src/java/ru/yandex/metrika/cdp/scheduler/cdp-scheduler-tasks.xml).
