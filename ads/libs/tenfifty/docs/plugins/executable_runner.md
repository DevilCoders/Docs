# Executable Runner
Плагин Executable Runner содержит композитное действие `build_run_executable`.

{% note warning %}

На данный момент плагин может некорректно работать на бэкенде tape, если конфигурация перезапускается с непустым `tape.state`.

{% endnote %}


## Композитное действие BuildRunExecutable (`build_run_executable`)
Собирает бинарь и запускает бинарь с аргументами.

**input:** список Dataset (может отсутствовать).

**output:** список Dataset (может отсутствовать).

* Возможно, в будущем в input и output будут поддерживаться и другие типы артефактов.

**parameters:**

* `artifact` (строка, обязательный) — путь до бинаря от корня Аркадии.
  * Пример: `ads/autobudget/action_model/scripts/collect_logs/collect_logs`
* `arcadia_revision` (необходим только для Nirvana) — ревизия аркадии.
* `build_type` (строка, необязательный) — тип сборки (`"release"`(default) или `"debug"`)
* `args:`
  * `command` (строка) — аргументы запуска бинаря.
  * `parameters` (dict) — доп. аргументы, встраиваемые в `command` (для удобного задания аргументов key: value)

Пример использования BuildRunExecutable (`build_run_executable`):

```yaml
MakeSamplesX:
    action: build_run_executable
    input:
        - output_CollectLogsX
    output:
        - output_MakeSamplesX
    do_after:
        - CollectLogsX
    parameters:
        build_type: "release"
        artifact: ads/autobudget/action_model/bin/action_make_samples
        arcadia_revision: 8551924
        args:
            command: --src-table $$input[0] --dst-table $$output[0]
            parameters:
                sample_clicks_threshold: 10
                sample_max_hours: 24
                sample_delay_hours: 6
                mode: 0

```
В собранной из `command` и `parameters` `args` конструкции вида `$$input[i]` и `$$output[i]` (пример: `$$input[0]`, `$$output[1]`) заменяются на пути артефактов на YT. Индекс в порядке перечисления артефактов в **input** и **output**.

### Детали реализации

{% list tabs %}

- Nirvana

    Для сборки используется кубик «BuildArcadiaProjectBlock» (см. [кубик в Нирване](https://nirvana.yandex-team.ru/operation/8253dbd7-a9a8-4600-b6ab-62d33d4cbffc)).

    Для каждого артефакта создается путь на YT, одинаковый (для одинаковых артефактов) только в пределах одного инстанса BuildRunExecutable. Из `endpoint'a` используемого входного артефакта вызывается кубик [`MRCopy`](https://nirvana.yandex-team.ru/operation/23762895-cf87-11e6-9372-6480993f8e34), в бинарь передаются пути (на YT) артефактов.

    После завершения BuildRunExecutable, для каждого [`MRCopy`](https://nirvana.yandex-team.ru/operation/23762895-cf87-11e6-9372-6480993f8e34) (созданного для каждого входного артефакта) вызывается [`MRDrop`](https://nirvana.yandex-team.ru/operation/9e9cfabb-63df-11e6-a050-3c970e24a776).

    Для выходных артефактов BuildRunExecutable вызывается [`GetMRTable`](https://nirvana.yandex-team.ru/operation/712225cb-cf5e-11e6-9372-6480993f8e34), чтобы артефакт появился в графе в качестве `endpoint'a`.

    [Пример графа](https://nirvana.yandex-team.ru/flow/a02e9e21-20fa-423d-9d76-a8ee9e519ef1).

- Tape

    Для сборки и запуска вызывается subprocess.check_call() c соответствующей командой.

    При сборке, subprocess вызывает ya make в директории бинаря (путь бинаря это параметр `artifact`)

    При запуске, subprocess исполняет `artifact` с собранной `args` из  `command` и `parameters`.

{% endlist %}
