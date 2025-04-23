# Хранение логов

## Коммунальный топик `deploy/logs` {#communal-topic}

Данный топик используется по умолчанию. Логи различных стейджей отгружаются в него без какой-либо группировки.
Записи из коммунального топика доступны в UI на странице **Stage** во вкладке **Logs**.

### YT {#yt}

{% note warning %}

[Не пишите в логи персональные данные](https://wiki.yandex-team.ru/security/awareness/skarif/policy/). Логи сливаются в YT в одну таблицу и доступны всем сотрудникам Яндекса.

{% endnote %}

Весь поток логов поставляется на YT-кластер Arnold (20 дней хранения) и Hahn (180 дней хранения) с помощью LogBroker и попадает в таблицы
* [https://yt.yandex-team.ru/arnold/navigation?path=//logs/deploy-logs&:](https://yt.yandex-team.ru/arnold/navigation?path=//logs/deploy-logs&:)
* [https://yt.yandex-team.ru/hahn/navigation?path=//logs/deploy-logs&:](https://yt.yandex-team.ru/hahn/navigation?path=//logs/deploy-logs&:)

Где:
* `//logs/deploy-logs/1d/YYYY-MM-DD` — дневной лог.
* `//logs/deploy-logs/30min/YYYY-MM-DDTHH:MM:SS` — 30-минутная поставка.

Для доступа к данным можно использовать несколько способов:

1. map- и reduce-операции в YT. Требует написания кода (чаще всего на Python), но позволяет гибко обрабатывать данные и строить разнообразные отчеты. [Документация](https://wiki.yandex-team.ru/yt/gettingstarted/);
1. [YQL](https://wiki.yandex-team.ru/yql/). Позволяет с помощью декларативного SQL-подобного языка запросов обрабатывать данные, хранящиеся в YT.

### YDB {#ydb}

Поток логов, отгружаемый в топик `deploy-logs`, поставляется также в YDB.
Срок хранения данных в YDB составляет `2 суток`, после чего таблицы с данными удаляются.

## Пользовательский топик {#custom-topic}

{% note warning %}

При использовании пользовательского топика логи не будут отображаться на вкладке **Logs** в UI Y.Deploy.

{% endnote %}

Возможно использование топика, отличного от коммунального — для каждого деплой-юнита выбор топика осуществляется независимо.
При этом топик в Logbroker и отгрузку данных в Logfeller необходимо настроить самостоятельно.

Для использования пользовательского топика необходимы следующие данные:

- идентификатор TVM приложения, от имени которого логи посылаются в топик.
- полное имя топика в Logbroker.
- секрет для авторизации через TVM (подробнее о секретах в Y.Deploy по [ссылке](../how-to/secrets.md)).

Настройки прокидываются в спецификацию деплой-юнита через [custom_topic_request](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8380085#L538):

- все поля внутри custom_topic_request являются обязательными для заполнения;
- селектор должен указывать на существующий в спеке секрет;

{% cut "Пример настроек в спеке" %}

```yaml
spec:
    deploy_units:
        deployUnitId:
            logbroker_config:
                custom_topic_request:
                    secret_selector:
                        alias: custom topic secret alias
                        id: client_secret
                    topic_name: deploy/custom_topic_test
                    tvm_client_id: 2000000
            replica_set:
                replica_set_template:
                    pod_template_spec:
                        spec:
                            secrets:
                                custom topic secret alias:
                                    delegation_token:
                                    secret_id:
                                    secret_version:
```

{% endcut %}

### Создание TVM приложения {#tvm}

В ABC-сервисе, от имени которого будут писаться логи, необходимо запросить сервис **Паспорт - TVM приложение** (категория **Безопасность**).
ID данного ресурса необходимо указать в настройках пользовательского топика в поле `tvm_client_id`.

В [секретнице](https://yav.yandex-team.ru/) для данного ресурса будет создан секрет с названием `tvm.secret.<tvm_client_id>`.

### Создание и настройка топика Logbroker {#logbroker-topic}

Logbroker имеет [веб-интерфейс](https://logbroker.yandex-team.ru/docs/interfaces/ui) и [консольный клиент](https://logbroker.yandex-team.ru/docs/interfaces/cli).

Управление топиками и другими ресурсами в рамках Logbroker осуществляется через [аккаунт](https://logbroker.yandex-team.ru/docs/concepts/resource_model#account).

Для осуществления действий в рамках аккаунта необходимо обладать набором соответствующих [прав](https://logbroker.yandex-team.ru/docs/concepts/security#authorization).

Создание топика через консольный клиент описано по [ссылке](https://logbroker.yandex-team.ru/docs/how_to/configuration#creating-topic).

{% note warning %}

Для передачи данных от имени TVM приложения ему необходимо выдать права `WriteTopic` на созданный топик.

{% endnote %}

### Сохранение данных через Logfeller {#logfeller}

Необходимо настроить три основных сущности (для примера приведены настройки коммунального топика Y.Deploy):

- стрим — переносчик данных через Logfeller ([пример](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/deploy_arnold_streams.json)).
- парсер — обработчик сырых данных перед сохранением ([пример](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/deploy-log-v2.json)).
- лог — хранилище данных ([пример](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/deploy_arnold_logs.json)).

{% note tip %}

Так как данные обогащаются и сохраняются в том же формате, что и при использовании коммунального топика, создание и настройка собственного парсера необязательны — можно переиспользовать парсер коммунального топика `deploy-log-v2`.

{% endnote %}

Все конфигурации Logfeller хранятся в [соответствующем репозитории](https://arcanum.yandex-team.ru/arc/trunk/arcadia/logfeller/configs).
Там же расположена подробная инструкция по конфигурации.

{% note warning %}

Для активации передачи данных из топика в Logfeller необходимо [добавить его в поставку](https://logbroker.yandex-team.ru/docs/how_to/configuration#configuring-yt-delivery).

{% endnote %}

### Настройка через Transfer Manager {#transfer-manager}

С недавнего времени доступна настройки передачи данных через [Transfer Manager](https://yc.yandex-team.ru/) в разделе **Data transfer**:

- [Инструкция по настройке через UI](https://wiki.yandex-team.ru/logfeller/kak-podkljuchitsja-cherez-ui/)
- [Transfer Manager API](https://cdc.n.yandex-team.ru/)