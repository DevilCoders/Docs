# Деплой сервисов

## Релиз сервисов в Arcadia CI

1. Открыть [релизы][microservices-releases] `frontend/projects/microservices` в Arcadia CI.
   Для релиза **Merge Queue** открыть [релизы][merge-queue-releases] `frontend/projects/microservices/services/merge-queue`.
2. На левой панели в списке Releases выбрать сервис для которого необходимо отвести релиз.
3. Нажать на кнопку **Run release** в правом верхнем углу.

   ![Выбор сервиса для отведения релиза](images/release-list.png)

4. Нажать на кнопку **Run release** в модальном окне.

   ![Запуск отведения релиза](images/start-release-flow.png)

[microservices-releases]: https://a.yandex-team.ru/projects/fei/ci/releases/timeline?dir=frontend%2Fprojects%2Fmicroservices&id=release
[merge-queue-releases]: https://a.yandex-team.ru/projects/mqspotlight/ci/releases/timeline?dir=frontend%2Fprojects%2Fmicroservices%2Fservices%2Fmerge-queue&id=release

### Сборка и деплой релиза в YDeploy

После отведения релиза запустится сборка Docker-образа. За процессом можно понаблюдать, перейдя по ссылке релизной ветки на странице релизов в Arcadia CI. Пример пайплайна:

![Docker image build](images/build-start.png)

После завершения сборки Docker-образа запустите в пайплайне кубик с деплоем:

![Deploy pipeline](images/deploy-microservice.png)

## Обновление версии Docker-образа через UI YDeploy

![Обновление Docker-образа в Ydeploy](images/docker-update.png)

После успешной сборки Docker-образа переходим к приложению сервиса в YDeploy и выбираем образ микросервиса (на примере — prosperity) и его версию.

## Обновление версии Docker-образа через CLI

Предварительно нужно установить и настроить утилиту [dctl].
Или использовать через `ya tool`.

Загрузить дамп сервиса:

```console
$ ya tool dctl get stage {ID сервиса} > config.yml
```

Обновить версию сервиса в `config.yml`.
В yaml-файле версия указывается в поле `tag` в секции `service`. В поле `description` секции `revision_info` поставить новую версию сервиса (например, `v2.37.0`), если менялась версия. Если версия не менялась (например, изменилась переменная среды), нужно кратко описать изменения.

Выгрузить обновлённый конфиг сервиса:

```
$ ya tool dctl put stage config.yml
```

[dctl]: https://wiki.yandex-team.ru/deploy/docs/dctl/

## ⚠️ Про `NAT64`

![Проверка NAT64](images/nat64-warning.png)

Обратите внимание, что некоторые сервисы должны иметь доступ к IPv4-ресурсам (галочка `NAT64`), например, для отправки нотификаций в Slack.

## ⚠️ Настройки секретов

![Необходимые секреты](images/secrets.png)

Обратите внимание, что все необходимые переменные окружения должны быть установлены. Важно именно имя переменной, а не имя секрета.
