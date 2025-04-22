# Работа с логами в GUI

В Y.Deploy логи доступны на странице **Stage** во вкладке **Logs**. Подробную информацию о механизме логирования и хранении логов смотрите в разделе [{#T}](../logs/index.md).

![https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-00-42.png](https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-00-42.png)

{% note warning %}

На данной вкладке отображаются только логи из [коммунального топика](../concepts/pod/sidecars/logs/logs.md#communal-topic).

{% endnote %}



## Включение стандартного механизма логирования {#activation}

Для включения стандартного механизма отгрузки логов:

{% list tabs %}

- UI

  Выставить переключатель `Logs` в `Enabled` в настройках выбранного workload'а в UI;

  ![https://jing.yandex-team.ru/files/slamur/Screenshot%20from%202021-11-08%2023-21-29.png](https://jing.yandex-team.ru/files/slamur/Screenshot%20from%202021-11-08%2023-21-29.png)

- Yaml-спецификация

  Указать `transmit_logs: true` через [dctl](../reference/tools/dctl.md) в спецификации workload'a:

  Пример спецификации:

  ```yaml
  spec:
    deploy_units:
      deploy_unit:
        multi_cluster_replica_set:
          replica_set:
            pod_template_spec:
              spec:
                pod_agent_payload:
                  spec:
                    workloads:
                      - id: 'workload'
                        transmit_logs: true
  ```

{% endlist %}

{% note warning %}

В случае, если отгрузка логов производится исключительно через библиотеки, требуется указать в спеке Deploy Unit [специальный флаг](#mandatory-logbroker-box).

{% endnote %}

## Фильтрация записей {#filter}

При помощи формы поиска можно отфильтровать записи по:

* **Deploy Unit** — в селекте выводятся все deploy units выбранного стейджа.
* **Log level** — в селекте поддерживается множественный выбор из набора базовых severity levels.
* Интервалу времени.
* Дополнительным условиям, задаваемым [в виде запроса](#query).

При изменении значений формы список записей обновляется автоматически. При изменении строки пользовательского запроса для его применения необходимо нажать на кнопку **Search**.

## Формирование запросов к логам в UI {#query}

В UI можно построить запрос с применением [полей из json-схемы](../concepts/pod/sidecars/logs/logs.md#format).

{% note alert %}

С целью минимизации нагрузки на YDB поддерживаются только простые `SELECT` запросы, потенциально "тяжелые" запросы с использованием `REGEXP`, `JOIN` и т.п. из UI **не поддерживаются**! Подобные запросы можно выполнить [к YT-таблицам](https://wiki.yandex-team.ru/users/golomolzin/cluster/projects/deploy/logs/structured/doc/#yt) при помощи YQL.

{% endnote %}

**Пример запроса:**

* `key = value1, value2, value3;` — условие на равенство, по OR.
* `key != value1, value2;` — условие на неравенство, по OR.

Зарезервированные символы: `"=,;!`
В случае необходимости использования символа `"` в запросе необходимо его экранировать, в случае необходимости использования символов `=,;!`, строку необходимо заключить в двойные кавычки (`"`)

**Пример запроса:**

```yaml
key = "literal value with \"quotas\"";
key = "literal value with other punctuation characters (=,;!)";
```

UI позволяет формировать запросы по вложенным json-полям, сохраненным в поле context, для этого запрос формируется к полю `context`, указав через точку (`.`) целевое поле.

**Пример запроса:**

`context.key1.key12 = value;`

![https://jing.yandex-team.ru/files/golomolzin/2020-04-15_12-51-05.png](https://jing.yandex-team.ru/files/golomolzin/2020-04-15_12-51-05.png)

## Сортировка записей {#sort}

По умолчанию используется `DESC` порядок сортировки по времени. При помощи клика на колонке Date порядок сортировки можно изменить:

![2020-04-12_21-11-16.png](https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-11-16.png)

## Просмотр записи {#view-record}

По умолчанию записи на странице выводятся в сокращенном формате — по двум строкам из сообщения. Для просмотра полного сообщения лога необходимо кликнуть на сообщении:

![https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-25-28.png](https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-25-28.png)

## Просмотр всех полей записи {#view-record-fields}

Для вывода всех полей записи, [сохраняемых в YDB](../concepts/pod/sidecars/logs/logs.md#schema), необходимо кликнуть на чекбоксе **JSON**:

![https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-27-57.png](https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-27-57.png)

Любое поле из выведенных можно применять при построении [запросов к логам](#query).

## Прямая ссылка на запись {#link-to-record}

При помощи клика на иконку ![https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-30-06.png](https://jing.yandex-team.ru/files/golomolzin/2020-04-12_21-30-06.png) в буфер обмена будет скопирована ссылка на выбранную запись. При открытии ссылки в браузере будет применен заданный фильтр, а также открыта страница с открытой выбранной записью.


## Новый интерфейс логов в Y.Deploy {#new-ui}

Включить новый интерфейс можно самостоятельно включить уже сейчас в настройках, для этого:

1. На странице [Y.Deploy](https://deploy.yandex-team.ru/) в правом верхнем углу перейдите в пользовательские настройки ![options](../_assets/settings.svg).
1. Включите опцию **New logs**.
1. Перезагрузите страницу.

![log_new_ui](../_assets/log_new_ui.png)

