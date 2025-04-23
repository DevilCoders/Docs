# Тасклеты

Тасклет - задача, запускаемая в sandbox и выполняющая некоторый набор действий. Подробнее про использование тасклетов в sandbox можно прочитать в [документации CI](https://docs.yandex-team.ru/ci/job-tasklet).

В morda-go и avocado используются как стандартные тасклеты - [ya_package_2](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/arcadia#ya_package_2,-ya_make), [ya_make](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/arcadia#ya_package_2,-ya_make), [infra_check_events](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/monitoring), [release_to_sandbox](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/releases#release-to-sandbox), [juggler_watch](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/monitoring#common/monitoring/juggler_watch) - так и сделанные [конкретно под нужны морды](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/projects/avocado). Дальнейшее описание касается проектных тасклетов, которые были написаны для нужд морды.

- [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets)
- [Файлы регистрации тасклетов](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/projects/avocado)
- [Прото-артефакты передаваемые между задачами](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/artifacts) (про автоматическую передачу артефактов можно прочитать в [документации CI](https://docs.yandex-team.ru/ci/flow#artifacts))
- Файлы конфигурации CI: [portal](https://a.yandex-team.ru/arc/trunk/arcadia/portal/a.yaml) (проверки в PR), [morda-go](https://a.yandex-team.ru/arc/trunk/arcadia/portal/morda-go/cmd/morda-go/a.yaml), [avocado](https://a.yandex-team.ru/arc/trunk/arcadia/portal/morda-go/cmd/avocado/a.yaml), [greenbox](https://a.yandex-team.ru/arc/trunk/arcadia/portal/morda-go/cmd/greenbox/a.yaml)
- [Секреты для работы тасклетов с различными API](https://yav.yandex-team.ru/secret/sec-01fxctddc9qp8pjjsh9k4hc6pw/explore/versions)

## Обновление тасклета

После обновления кода тасклета необходимо его собрать (на Linux машине) и залить собранный бинарник в sandbox (как это сделать - [документация CI](https://docs.yandex-team.ru/ci/job-tasklet)). После этого необходимо проставить версию sandbox ресурса в файл регистрации тасклета.

Если после тестирования тасклета все хорошо, надо не забыть зарелизить его в stable в sandbox.

## Добавление нового тасклета

Для добавления нового тасклета нужно добавить описание в proto формате, написать имплементацию, собрать (на Linux машине) и залить собранный бинарник в sandbox, добавить или обновить файл регистрации тасклета. Подробно про все шаги можно прочитать в официальной [документации CI](https://docs.yandex-team.ru/ci/job-tasklet).

После коммита тасклета в репозиторий появляется возможность использовать его в разнообразных flow. Для этого необходимо добавить его в один или несколько файлов конфигурации CI отдельным шагом исполнения (job в описании flow).

Если после тестирования тасклета все хорошо, надо не забыть зарелизить его в stable в sandbox.

## Описание тасклетов

Тут приводится описание тасклетов, реализованных на языке Python для CI процессов морды.

### create_beta_from_template

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/create_yappy_from_template)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/create_yappy_from_template/proto/create_yappy_from_template.proto)

Создает Yappy бету на основе заранее подготовленного шаблона и дожидается ее перехода в состояние `Consistent`. Если запускается из PR flow, то добавляет бейдж с ссылкой на созданную бету в description соответствующего PR. Используется в PR flow для создания беты с изменениями из PR.

### run_teamcity_build

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/run_teamcity_build)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/run_teamcity_build/proto/run_teamcity_build.proto)

Запускает сборку в teamcity и дожидается ее завершения. В случае неуспешного завершения сборки результат запуска тасклета также будет неуспешным. Используется в PR flow и релизных flow для запуска тестов из перлового репозитория.

### remove_yappy

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/remove_yappy)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/remove_yappy/proto/remove_yappy.proto)

Удаляет Yappy бету. Используется в clean up секции PR flow. В коде тасклета есть проверка, что если запуск происходит в PR flow, и ревью не закрыто, то бета не удаляется. Сделано это по той причине, что с точки зрения CI каждый PR flow - отдельная сущность, определяемая, в том числе, по diff_set_id. Без отдельной проверки при каждом обновлении PR происходило бы удаление беты, которое, в том числе, могло случиться уже после обновления ресурсов из нового diff set.

### create_release_ticket

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/create_release_ticket)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/create_release_ticket/proto/create_release_ticket.proto)

Создает релизный тикет, куда линкуются задачи и коммиты, которые появились с последнего запуска релиза и добавляются наблюдателями дежурные указанных сервисов. Используется в релизных flow, в других типах flow не имеют особого смысла.

В output отдает артефакт типа `ReleaseTicket`.

### set_release_ticket_status

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/set_release_ticket_status)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/set_release_ticket_status/proto/set_release_ticket_status.proto)

Обновляет статус релизного тикета на указанный в конфиге. Падает, если переход из текущего статуса в новый не существует. Используется в релизных flow.

В input ожидает артефакт типа `ReleaseTicket`.

### send_telegram_message

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/send_telegram_message)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/send_telegram_message/proto/send_telegram_message.proto)

Отправляет сообщение произвольного содержания в telegram с помощью `nyanBot`. Используется в релизных flow для уведомления об основных шагах релиза.

### activate_sandbox_release_for_service

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/activate_sandbox_release_for_service)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/activate_sandbox_release_for_service/proto/activate_sandbox_release_for_service.proto)

Если для Nanny сервиса настроена тикетная интеграция, то после релиза ресурса в sandbox создается Nanny тикет на обновление ресурса в зависимых от него сервисах. Данный тасклет по описанию sandbox ресурса находит его Nanny тикет, в тикете находит указанный в конфиге сервис и создает activate событие для данного сервиса, передавая указанные activate и prepare рецепты. Используется в релизных flow для активации выкладки ресурса на соответствующий Nanny сервис.

В output отдает артефакт типа `NannySnapshot`, необходимый для работы других тасклетов, связанных с Nanny.

### wait_for_nanny_snapshot_state

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/wait_for_nanny_snapshot_state)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/wait_for_nanny_snapshot_state/proto/wait_for_nanny_snapshot_state.proto)

Дожидается перехода snapshot'а Nanny сервиса в указанное в конфиге состояние. Используется в релизных flow для ожидания завершения выкладки или для ожидания перехода в состояние `Activating` перед ручным подтверждением активации.

В input ожидает артефакты типа `NannySnapshot`.

### nanny_activate_one_host

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/nanny_activate_one_host)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/nanny_activate_one_host/proto/nanny_activate_one_host.proto)

Для snapshot'а выбирает первый доступный инстанс в указанной локации и переводит его в состояние `Active`, после чего дожидается завершения активации. Используется в релизных flow как своеобразный `prestable` перед активацией локаций.

В input ожидает артефакты типа `NannySnapshot`.

### nanny_activate_location

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/nanny_activate_location)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/nanny_activate_location/proto/nanny_activate_location.proto)

Для snapshot'а при выкладке с рецептом locationwise и ручным подтверждением прожимает `Confirm` для соответствующей задачи активации локации. Используется в релизных flow для подтверждения выкладки на локацию.

В input ожидает артефакты типа `NannySnapshot`.

### nanny_activate_snapshot

* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/nanny_activate_snapshot)
* [Описание input и output](https://a.yandex-team.ru/arc/trunk/arcadia/portal/avocado/tasklets/nanny_activate_snapshot/proto/nanny_activate_snapshot.proto)

Для snapshot'а запрашивает его перевод в состояние `Active` с указанными в конфиге рецептами для `activate` и `prepare` и проставляет snapshot в current. Не дожидается перехода в запрошенное состояние, для этого используется тасклет `wait_for_nanny_snapshot_state`. Используется в rollback flow для активации ранее выкаченной версии.

В input ожидает артефакты типа `NannySnapshot`.
