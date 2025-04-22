# Релиз Zeroline

## Как отвести релиз в Arcadia CI

_Внимание: версия релиза (docker-образа) и версия, указанная в файле [package.json][zeroline-package-json], могут не совпадать. Так как инкремент версий релизов происходит независимо от изменений версии в package.json._

### Запуск релиза

- открываем страницу с [релизами Zeroline][zeroline-releases] в Arcadia CI;

- на левой панели в списке _Releases_ выбираем сервис, для которого необходимо отвести релиз;

- нажимаем на кнопку **Run release** в правом верхнем углу, релиз будет отведен для последнего коммита:

  ![Выбор сервиса для отведения релиза](images/list-of-releases-and-commits.png)

- в модальном окне в поле _Release flow_ выбираем _zeroline-release-flow_ и нажимаем на кнопку **Run release**:

  ![Запуск отведения релиза](images/run-release.confirm-dialog.png)

### Сборка Docker-образа

- после запуска релиза запустится сборка Docker-образа:

  ![Docker image build progress](images/build-docker-image.progress.png)

- переходим по ссылке _Релиз Zeroline #<версия>_, если хотим посмотреть на ход текущей задачи:

  ![Docker image build progress](images/build-docker-image.see-details.png)

- чтобы перейти в sandbox-задачу, собирающую docker-образ, нажимаем на букву **S**:

  ![Docker image build job running](images/build-docker-image.job-running.png)

- сборка docker-образа происходит в задаче _YA_PACKAGE_2_ на основе файлов _[ya-package.json][ya-package-json]_ и _[Dockerfile][dockerFile]:_

   ![Docker image build sandbox task](images/build-docker-image.sandbox-task.png)

### Выкладка Docker-образа на zeroline (production) в Y.Deploy

- после завершения сборки Docker-образа релиз будет приостановлен в ожидании ручного подтверждения _(Waiting For Manual Trigger)_ выкладки на production:

  ![Release to stable waiting for manual trigger](images/release-to-stable.waiting-for-manual-trigger.png)

- переходим по ссылке _Релиз Zeroline #<версия>_, чтобы запустить выкладку на **zeroline** (production):

  ![Release to stable job waiting for run](images/release-to-stable.job-waiting-for-run.png)

- нажимаем на кнопку _Play_ и подтверждаем выкатку на **zeroline** (production), нажав **Yes**:

  ![Release to stable confirm](images/release-to-stable.confirm.png)

- начинается выкатка _(Release to stable);_

- можно наблюдать за ходом выкладки, если перейти по ссылке _Релиз Zeroline #<версия>:_

  ![Release to stable job running](images/release-to-stable.job-running.png)

- выкладка на Y.Deploy сопровождается созданием соответствующего «тикета» в разделе _[Deploy tickets][deploy-tickets]_ сервиса **zeroline**:

  ![Deploy ticket](images/deploy.ticket.png)

- после того, как выкладка будет завершена, в [истории операций][zeroline-history] с **zeroline** можно будет увидеть последнее обновление:

  ![Deploy done history](images/deploy.history-done.png)

- обновление **zeroline** (production) завершено:

  ![Release to stable all jobs done](images/release-to-stable.all-jobs-done.png)

### Релиз успешно завершен!

  ![Release to stable done](images/release-to-stable.done.png)

[zeroline-package-json]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/zeroline/package.json

[zeroline-releases]: https://a.yandex-team.ru/projects/zeroline/ci/releases/timeline?dir=frontend%2Fprojects%2Finfratest%2Fservices%2Fzeroline&id=release

[ya-package-json]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/zeroline/ya-package.json

[dockerfile]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/zeroline/Dockerfile

[deploy-tickets]: https://deploy.yandex-team.ru/stages/zeroline/deploy-tickets?stageId=zeroline&ticketStatuses=closed%2Ccommitted%2CinProgress%2ConHold%2Cpending%2Cskip%2Cunknown%2Cwait%2CwaitingForApprove%2CwaitingForCommit

[zeroline-history]: https://deploy.yandex-team.ru/stages/zeroline/history
