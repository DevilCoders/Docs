# How release new LXC container

1. Modify `resources/custom_script.sh` - add your libraries, or something else
2. `cd SdcLxcContainerForCI` and call **run.bash**
```
markperez@sdc-vm-heavy-3:~/sync-repo2/sandbox/projects/sdc/SdcLxcContainerForCI$ ./run.bash
Ok
2022-05-05 14:37:53 INFO 1 file (257.42MiB) to upload
2022-05-05 14:37:53 INFO Uploading task #1299902051 created: https://sandbox.yandex-team.ru/task/1299902051
2022-05-05 14:38:22 INFO Resource is in READY state
2022-05-05 14:39:02 INFO Task of type SDC_LXC_CONTAINER_FOR_CI created: https://sandbox.yandex-team.ru/task/1299902467
2022-05-05 14:39:08 INFO Task started successfully.
2022-05-05 14:39:08 INFO Waiting for the task to finish
2022-05-05 14:39:09 INFO Task status is ASSIGNED
2022-05-05 14:39:22 INFO Task status is PREPARING
2022-05-05 14:39:25 INFO Task status is EXECUTING
2022-05-05 14:39:38 INFO Task status is STOPPING
2022-05-05 14:39:41 INFO Task status is WAIT_TASK
2022-05-05 14:55:23 INFO Task status is ENQUEUING
2022-05-05 14:55:26 INFO Task status is ASSIGNED
2022-05-05 14:55:38 INFO Task status is FINISHING
2022-05-05 14:55:44 INFO Task status is SUCCESS
{"task": {"owner": "markperez", "type": "SDC_LXC_CONTAINER_FOR_CI", "id": 1299902467, "execution_status": "SUCCESS"}, "resource": {"attributes": {"binary_age": "8", "commit_revision": "-1", "taskbox_enabled": "True", "backup_task": true, "binary_hash": "54976086ede2fb2ff2770709c72b38d4"}, "task": {"status": "WAIT_RES", "url": "https://sandbox.yandex-team.ru/api/v1.0/task/1299902051", "id": 1299902051}, "type": "SANDBOX_TASKS_BINARY", "id": 3064038543}}
```
4. Wait until sandbox task finished
5. Visit sandbox task url (grab it from log)
6. Go-to child tasks -> `SANDBOX_LXC_IMAGE` -> press release button
