# Релиз Merge Queue Spotlight

## Отведение релиза в Arcadia CI

1. Открыть [релизы][merge-queue-spotlight-releases] `frontend/projects/infratest/services/merge-queue-spotlight` в Arcadia CI.
2. На левой панели в списке Releases выбрать сервис для которого необходимо отвести релиз.
3. Нажать на кнопку **Run release** в правом верхнем углу.

   ![Выбор сервиса для отведения релиза](images/release-list.png)

4. В модальном окне в поле Release flow выбрать _mq-spotlight-release-flow_  и нажать на кнопку **Run release**.

   ![Запуск отведения релиза](images/start-release-flow.png)

[merge-queue-spotlight-releases]: https://a.yandex-team.ru/projects/mqspotlight/ci/releases/timeline?dir=frontend%2Fprojects%2Finfratest%2Fservices%2Fmerge-queue-spotlight&id=release

### Сборка и деплой релиза в YDeploy

После отведения релиза запустится сборка Docker-образа. За процессом можно понаблюдать, перейдя по ссылке _Релиз Merge Queue Spotlight#<версия>_ на странице релизов в Arcadia CI. Пример пайплайна:

![Docker image build](images/build-start.png)

В пайплайне собранный Docker-образ автоматически деплоится на приёмку https://mqs-beta.si.yandex-team.ru для тестирования.

После тестирования релиз можно запустить деплой релиза на продакшен.

![Deploy pipeline](images/deploy-service.png)
