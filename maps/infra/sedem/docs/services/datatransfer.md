# Настройка Data Transfer для доставки логов на YT

{% note tip "TL;DR" %}

1. Создать / подготовить YT-аккаунт
2. Создать / настроить топик в Logbroker
3. Заполнить секцию `datatransfer` в sedem-конфиге сервиса
4. Настроить отправку логов в Logbroker в вашем сервисе

{% endnote %}

## 1. YT account { #yt-account }

Создайте аккаунт для своего сервиса [hahn/accounts](https://yt.yandex-team.ru/hahn/accounts/)

- **Create account** в правом верхнем углу страницы
- В качестве имени аккаунта укажите имя вашего сервиса

В созданном аккаунте запросите права (**Request permissions**) `Use` для группы [LogFeller](https://abc.yandex-team.ru/services/logfeller/)

**TBD: request quota**

## 2. Logbroker { #logbroker }

1. Для создания топика выберете или создайте аккаунт [logbroker/accounts](https://logbroker.yandex-team.ru/logbroker/accounts)
2. Внутри аккаунта создайте топик для отправки логов: `New resource -> Topic`
3. В созданном топике подключите YT Delivery: `shared/hahn-logfeller`

Подробную документацию по **Logbroker** можно найти на [logbroker.yandex-team.ru/docs/](https://logbroker.yandex-team.ru/docs/)

## 3. Sedem-config { #datatransfer-sedem-config }

Создание **Data Transfer** пайплайна настраивается через sedem-конфиг

*NB: на текущий момент поддержан только LogFeller трансфер — из Logbroker в YT*

```yaml
datatransfer:  # section to setup datatransfer pipeline
  logfeller:   # section to setup LogFeller
    transfername:  # transfer name and prefix for source and target endpoints
      topic: maps/infra-super-topic
      log_name: maps/infra-super-log-name
      fields: [{"name": "timestamp", "type": "YT_TYPE_TIMESTAMP", "sort":  true},
               {"name": "value",     "type": "YT_TYPE__INT64"}]
      lifetime: 14d
      yt_account: logfeller
```
* `topic` - имя топика в Logbroker
* `log_name` - путь лога в YT (будет записан Logfeller'ом в `/logs/<log_name>`)
* `fields` - описывает схему сообщений в логе
    * `name` - имя поля в JSON сообщении из Logbroker топика и имя поля в итоговой YT таблице лога
    * `type` - тип YT поля, список полей в [protobuf API LogFeller](https://a.yandex-team.ru/arcadia/cloud/bitbucket/private-api/yandex/cloud/priv/datatransfer/v1/endpoint/logfeller.proto?rev=r9708552#L132-149)
    * `sort` - делает итоговое поле в YT таблице sortable, по дефолту `false`
* `lifetime` - настройка lifetime из target LogFeller endpoint-а, регулирует время жизни таблиц лога
* `yt_account` - аккаунт с квотой для записи логов в YT

Изменения будут применены после коммита sedem-конфига.

Подробную документацию по **Data Transfer** можно найти на [docs.yandex-team.ru/cloud/data-transfer/](https://docs.yandex-team.ru/cloud/data-transfer/)

## 4. Send logs to Logbroker { #send-logs-to-logbroker }

Если вы используете карточный базовый образ, то настроить отправку логов в Logbroker можно через unified-agent.
Инструкция есть в [baseimage/README.md#unified-agent](https://a.yandex-team.ru/arcadia/maps/infra/baseimage/README.md#unified-agent)

Для Yacare сервисов есть готовое решение сериализации логов в syslog для unified-agent из базового образа карт.
[yacare/README.md#logbroker](https://a.yandex-team.ru/arcadia/maps/infra/yacare#logbroker)
