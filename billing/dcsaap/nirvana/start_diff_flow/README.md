Пример запуска Nirvana Workflow
===============================

`--sync` - ждём окончания работы операции
`--result` - переопределяем параметр `output_table` в workflow

```sh
➜ ya make
Ok

➜ ./start_diff_flow \
    --nirvana-oauth-token "XXX" \
    --workflow-instance-id "01a1753e-176c-4f1c-9f4a-7f7ff923184b" \
    --workflow-id "39862e77-cb9c-449f-b3e2-2edcbfa5bf4f" \
    --sync 1 \
    --result "//home/balance/dev/shorrty/diff-from-api"
[2019-11-28 18:29:50,303] INFO: started ...
[2019-11-28 18:29:51,217] INFO: new instance: ba14b3f4-27ef-4740-ba5d-e2bfe8bce049
[2019-11-28 18:29:51,558] INFO: parameters: [{'parameter': 'keys', 'value': 'product_name page_service_code'}, {'parameter': 'columns', 'value': 'turnover reward base'}, {'parameter': 'table1_path', 'value': '//home/balance/dev/tamirok/new'}, {'parameter': 'table2_path', 'value': '//home/balance/dev/tamirok/old'}, {'parameter': 'yt_cluster', 'value': 'hahn'}, {'parameter': 'output_table', 'value': '//home/balance/dev/shorrty/nirvana_new_old_diff3'}, {'parameter': 'encryptedOauthToken', 'value': 'robot-balance-ar-tst-yql'}]
[2019-11-28 18:29:52,605] INFO: started: ba14b3f4-27ef-4740-ba5d-e2bfe8bce049
[2019-11-28 18:29:52,755] INFO:  - state: {'status': 'running', 'result': 'undefined', 'progress': 0.0, 'message': '', 'details': '', 'started': '2019-11-28T18:29:52+0300', 'blocks': [], 'workflowInstanceId': 'ba14b3f4-27ef-4740-ba5d-e2bfe8bce049'}
[2019-11-28 18:30:02,838] INFO:  - state: {'status': 'running', 'result': 'undefined', 'progress': 0.0, 'message': '', 'details': '', 'started': '2019-11-28T18:29:52+0300', 'blocks': [], 'workflowInstanceId': 'ba14b3f4-27ef-4740-ba5d-e2bfe8bce049'}
[2019-11-28 18:30:12,904] INFO:  - state: {'status': 'running', 'result': 'undefined', 'progress': 0.0, 'message': 'Finished 0/1.', 'details': 'Waiting: 0 / Running: 0 / Succeeded: 0 / Failed: 0 / Cancelled: 0 / Skipped: 0', 'started': '2019-11-28T18:29:52+0300', 'blocks': [], 'workflowInstanceId': 'ba14b3f4-27ef-4740-ba5d-e2bfe8bce049'}
...
[2019-11-28 18:35:44,938] INFO:  - state: {'status': 'running', 'result': 'undefined', 'progress': 0.0, 'message': 'Finished 0/1.', 'details': 'Waiting: 0 / Running: 0 / Succeeded: 0 / Failed: 0 / Cancelled: 0 / Skipped: 0', 'started': '2019-11-28T18:29:52+0300', 'blocks': [], 'workflowInstanceId': 'ba14b3f4-27ef-4740-ba5d-e2bfe8bce049'}
[2019-11-28 18:35:55,423] INFO:  - state: {'status': 'completed', 'result': 'success', 'progress': 1.0, 'message': 'Finished 1/1.', 'details': 'Waiting: 0 / Running: 0 / Succeeded: 1 / Failed: 0 / Cancelled: 0 / Skipped: 0', 'started': '2019-11-28T18:29:52+0300', 'completed': '2019-11-28T18:35:52+0300', 'blocks': [], 'workflowInstanceId': 'ba14b3f4-27ef-4740-ba5d-e2bfe8bce049'}
[2019-11-28 18:36:05,432] INFO: done.
```
