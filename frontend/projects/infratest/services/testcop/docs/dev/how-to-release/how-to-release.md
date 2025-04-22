# Релиз Тесткопа

## Как отвести релиз в Arcadia CI

_Внимание: версия релиза (docker-образа) и версия, указанная в файле [package.json][testcop-package-json], могут не совпадать. Так как инкремент версий релизов происходит независимо от изменений версии в package.json._

### Запуск релиза

- открываем страницу с [релизами Тесткопа][testcop-releases] в Arcadia CI;

- на левой панели в списке _Releases_ выбираем сервис, для которого необходимо отвести релиз;

- нажимаем на кнопку **Run release** в правом верхнем углу, релиз будет отведен для последнего коммита:

  ![Выбор сервиса для отведения релиза](images/list-of-releases-and-commits.png)

- в модальном окне в поле _Release flow_ выбираем _testcop-release-flow_ и нажимаем на кнопку **Run release**:

  ![Запуск отведения релиза](images/run-release.confirm-dialog.png)

### Сборка Docker-образа

- после запуска релиза запустится сборка Docker-образа:

  ![Docker image build progress](images/build-docker-image.progress.png)

- переходим по ссылке _Релиз Тесткопа #<версия>_, если хотим посмотреть на ход текущей задачи:

  ![Docker image build progress](images/build-docker-image.see-details.png)

- чтобы перейти в sandbox-задачу, собирающую docker-образ, нажимаем на букву **S**:

  ![Docker image build job running](images/build-docker-image.job-running.png)

- сборка docker-образа происходит в задаче _YA_PACKAGE_2_ на основе файлов _[ya-package.json][ya-package-json]_ и _[Dockerfile][dockerFile]:_

   ![Docker image build sandbox task](images/build-docker-image.sandbox-task.png)

### Выкладка Docker-образа на testcop-beta в Y.Deploy

- после сборки Docker-образа начнется его автоматическая выкладка на **testcop-beta** в Y.Deploy _(стадия Release to prestable):_

  ![Release to prestable progress](images/release-to-prestable.progress.png)

- аналогично можно наблюдать за ходом выкладки, если перейти по ссылке _Релиз Тесткопа #<версия>:_

  ![Release to prestable job running](images/release-to-prestable.job-running.png)

- выкладка на Y.Deploy сопровождается созданием соответствующего «тикета» в разделе _[Deploy tickets][deploy-beta-tickets]_ сервиса **testcop-beta**:

  ![Deploy-beta ticket](images/deploy-beta.ticket.png)

- после того, как выкладка будет завершена, в [истории операций][testcop-beta-history] с **testcop-beta** можно будет увидеть последнее обновление:

  ![Deploy-beta done history](images/deploy-beta.history-done.png)

### Выкладка Docker-образа на testcop (production) в Y.Deploy

- после завершения выкладки Docker-образа на **testcop-beta** _(Release to prestable)_ релиз будет приостановлен в ожидании ручного подтверждения _(Waiting For Manual Trigger)_ выкладки на production:

  ![Release to stable waiting for manual trigger](images/release-to-stable.waiting-for-manual-trigger.png)

- переходим по ссылке _Релиз Тесткопа #<версия>_, чтобы запустить выкладку на **testcop** (production):

  ![Release to stable job waiting for run](images/release-to-stable.job-waiting-for-run.png)

- нажимаем на кнопку _Play_ и подтверждаем выкатку на **testcop** (production), нажав **Yes**:

  ![Release to stable confirm](images/release-to-stable.confirm.png)

- начинается выкатка _(Release to stable):_

  ![Release to stable progress](images/release-to-stable.progress.png)

- аналогично можно наблюдать за ходом выкладки, если перейти по ссылке _Релиз Тесткопа #<версия>:_

  ![Release to stable job running](images/release-to-stable.job-running.png)

- выкладка на Y.Deploy сопровождается созданием соответствующего «тикета» в разделе _[Deploy tickets][deploy-prod-tickets]_ сервиса **testcop**:

  ![Deploy ticket](images/deploy.ticket.png)

- после того, как выкладка будет завершена, в [истории операций][testcop-prod-history] с **testcop** можно будет увидеть последнее обновление:

  ![Deploy done history](images/deploy.history-done.png)

- обновление **testcop** (production) завершено:

  ![Release to stable all jobs done](images/release-to-stable.all-jobs-done.png)

### Релиз успешно завершен!

  ![Release to stable done](images/release-to-stable.done.png)

[testcop-package-json]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/testcop/package.json

[testcop-releases]: https://a.yandex-team.ru/projects/testcop/ci/releases/timeline?dir=frontend%2Fprojects%2Finfratest%2Fservices%2Ftestcop&id=release

[ya-package-json]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/testcop/ya-package.json

[dockerfile]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/testcop/Dockerfile

[deploy-beta-tickets]: https://deploy.yandex-team.ru/stages/testcop-beta/deploy-tickets?stageId=testcop-beta&ticketStatuses=closed%2Ccommitted%2CinProgress%2ConHold%2Cpending%2Cskip%2Cunknown%2Cwait%2CwaitingForApprove%2CwaitingForCommit

[deploy-prod-tickets]: https://deploy.yandex-team.ru/stages/testcop/deploy-tickets?stageId=testcop&ticketStatuses=closed%2Ccommitted%2CinProgress%2ConHold%2Cpending%2Cskip%2Cunknown%2Cwait%2CwaitingForApprove%2CwaitingForCommit

[testcop-beta-history]: https://deploy.yandex-team.ru/stages/testcop-beta/history

[testcop-prod-history]: https://deploy.yandex-team.ru/stages/testcop/history
