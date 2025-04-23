# Мониторинги Merge Queue

## monitorado.custom.mqspotlight.merge-queue_state_monitor_err

Очередь задач для MQ хранится в базе в виде списка джоб с определенным набором параметров, а исполняются задачи по-прежнему в sandbox. Очевидно, что состояния таски в sandbox и джобы в базе должны быть синхронизированы. Для того, чтобы гарантировать синхронизацию состояний, раз в n минут срабатывает `state-monitor` и в случае расхождения состояний в базе и sandbox, состояния синхронизируются и отправляется сигнал в [yasm](https://yasm.yandex-team.ru/template/panel/fei-alerts/abc=mqspotlight/). В случае превышения порога срабатывает алерт и заводится тикет в `INFRADUTY`. Если тикет был заведен, значит что-то пошло не так:

1. Sandbox задача по каким-то причинам не была запущена.
2. Не долетел хук от завершенной sandbox/trendbox задачи и сервис считает, что эта задача до сих пор executing.
3. Не смогли обновить джобу в базе при запуске MQ-задачи и в джобе id задачи отсутствует.
4. MQ-сервис по каким-то причинам упал перед запуском следующей задачи и очередь зависла, т.к. все задачи в базе находятся в состоянии enqueued.

В случае, если нет какой-то явной аварии, которая могла послужить причиной тикета (отвалился sandbox, отвалилась база, отвалился ydeploy, etc.), идем дебажить:

1. Проверяем по `debug.log` mq-таски, были ли отправлены необходимые хуки (для этого есть [соответствующие логи](https://a.yandex-team.ru/arc_vcs/sandbox/projects/sandbox_ci/sandbox_ci_merge_queue/__init__.py?rev=5919686#L1177 ))
2. Идем в [логи MQ-сервиса](https://deploy.yandex-team.ru/stage/merge-queue/logs) и смотрим, [какие хуки](https://github.yandex-team.ru/search-interfaces/microservices/blob/v2.14.2/services/merge-queue/modules/listeners/sandbox/task.js) прилетали в сервис, грепая по `merge-queue\:sandbox\:task.*number {N}`, где N - номер пулл-реквеста, в котором были проблемы
3. В логах из п.2 грепаем по `merge-queue\:job-queue\:state-monitor state-error` и ищем в логах место, в котором произошло расхождение состояний в sandbox и в merge-queue
4. В зависимости от типа проблемы, идем разбираться в `ydeploy\sandbox`
