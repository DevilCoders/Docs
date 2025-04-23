# Отгрузка системных логов

Начиная с версии [подового агента 104-1](https://deploy.yandex-team.ru/docs/reference/pod-agent-releases#) и [Runtime version 12](https://deploy.yandex-team.ru/docs/reference/patchers-revision#runtime-version-12) появилась возможность отгружать системные логи подового агента. Системные логи содержат события хуков (start, stop, destroy, liveness, readiness, init) для пользовательских ворклоудов и боксов.

## Включение через UI {#activate}

1. В настройках деплой юнита выбираем **Runtime Revision 12**:
    ![https://jing.yandex-team.ru/files/dkochetov/screenshot_146.png](https://jing.yandex-team.ru/files/dkochetov/screenshot_146.png)
1. Выбираем релиз подового агента **104-1** или выше:
    ![https://jing.yandex-team.ru/files/dkochetov/screenshot_147.png](https://jing.yandex-team.ru/files/dkochetov/screenshot_147.png)
1. В настройках деплой юнита включаем отгрузку системных логов **Transmit system logs policy**:
    ![https://jing.yandex-team.ru/files/dkochetov/screenshot_145.png](https://jing.yandex-team.ru/files/dkochetov/screenshot_145.png)

Теперь у стейджа на вкладке **Logs** для конкретного деплой юнита можно отфильтровать системные логи по `logger_name=pod_agent_system_logs`.
![https://jing.yandex-team.ru/files/dkochetov/screenshot_149.png](https://jing.yandex-team.ru/files/dkochetov/screenshot_148.png)


### Фильтрация системных логов на UI по workload_id/box_id {#gui-filter-wl-box}

Фильтрация системных логов на UI по workload_id/box_id/итд будет возможна после реализации [DEPLOY-5615](https://st.yandex-team.ru/DEPLOY-5615).

## Описание поля message {#message}

### Описание поля message для container hook {#container-hook}

```json
"message": {
    "state": "EContainerState_EXITED",
    "return_code": 0,
    "stderr_tail": "",
    "stdout_tail": "",
    "fail_reason": "",
    "start_time": 1647808395000000,
    "death_time": 1647808395000000,
    "object_type": "WORKLOAD",
    "container_type": "READINESS",
    "init_num": 0,
    "object_id_or_hash": "server1_workload"
}
```

Где:

* `state` — состояние выполнения container хука. Возможные значения описаны [тут](https://arcanum.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L1232).
* `return_code` — код возврата container хука.
* `stderr_tail` — на текущий момент всегда пустая строка.
* `stdout_tail` — на текущий момент всегда пустая строка.
* `start_time` — таймстемп начала выполнения хука.
* `death_time` — таймстемп окончания выполнения хука.
* `fail_reason` — содержит причину ошибки выполнения.
* `object_type` — тип обьекта для которого выполняется хук. Возможные значения: WORKLOAD, BOX.
* `container_type` — тип хука(START, READINESS, LIVENESS, STOP, DESTROY, INIT).
* `init_num` — номер выполненного init hook. Данное поле имеет значимость только в случае если тип хука INIT.
* `object_id_or_hash` — id объекта, для которого выполняется хук.

### Описание поля message для http hook {#http-hook}

```json
"message": {
    "state": "EHttpGetState_FAILURE",
    "fail_reason": "",
    "inner_fail_reason": "readiness probe failed: HTTP request to http2://localhost:82/ping: Connection refused",
    "start_time": 1647809071043555,
    "death_time": 1647809071245540,
    "object_type": "WORKLOAD",
    "id": "server1_workload",
    "hook_type": "READINESS"
}
```

Где:

* `state` — состояние выполнения http хука. Возможные значения описаны [тут](https://arcanum.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L1360).
* `fail_reason`, `inner_fail_reason` — содержат причину ошибки выполнения хука.
* `start_time` — таймстемп начала выполнения хука.
* `death_time` — таймстемп окончания выполнения хука.
* `object_type` — тип обьекта для которого выполняется хук, здесь всегда значение WORKLOAD.
* `container_type` — тип хука(READINESS, LIVENESS, STOP, DESTROY).
* `id` — id объекта, для которого выполняется хук.

### Описание поля message для tcp hook {#tcp-hook}

```json
"message": {
    "state": "ETcpCheckState_FAILURE",
    "fail_reason": "readiness probe failed: TCP request to [::1]:80: Connection refused",
    "start_time": 1647809371243002,
    "death_time": 1647809371444965,
    "object_type": "WORKLOAD",
    "id": "server1_workload",
    "hook_type": "READINESS"
}
```

Где:

* `state` — состояние выполнения tcp хука. Возможные значения описаны [тут](https://arcanum.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L1382).
* `fail_reason` — содержит причину ошибки выполнения хука.
* `start_time` — таймстемп начала выполнения хука.
* `death_time` — таймстемп окончания выполнения хука.
* `object_type` — тип обьекта для которого выполняется хук, здесь всегда значение WORKLOAD.
* `id` — id объекта для которого выполняется хук.
* `hook_type` — тип хука(READINESS, LIVENESS, STOP, DESTROY).

### Описание поля message для unix signal hook {#unix-signal-hook}

```json
"message": {
    "state": "EUnixSignalState_SUCCESS",
    "fail_reason": "",
    "send_time": 1647809071245540,
    "object_type": "WORKLOAD",
    "id": "server1_workload"
}
```

Где:

* `state` — состояние выполнения хука. Возможные значения описаны [тут](https://arcanum.yandex-team.ru/arc/trunk/arcadia/infra/libs/logger/protos/events.ev?rev=r9233088#L215).
* `fail_reason` — содержит причину ошибки выполнения хука.
* `send_time` — таймстемп посыла сигнала.
* `object_type` — тип объекта для которого выполняется хук, здесь всегда значение WORKLOAD.
* `id` — id объекта для которого выполняется хук.

