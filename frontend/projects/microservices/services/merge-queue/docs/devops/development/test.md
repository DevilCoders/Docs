# Тестирование Merge Queue

## Запуск сервиса
Запускаем MQ-микросервис, используя тестовый Стартрек:
```bash
STARTREK_ENTRYPOINT=https://st-api.test.yandex-team.ru npm run merge-queue
```
По умолчанию сервис запускается на `localhost:3000`.
Порт можно переопределить переменной окружения `QLOUD_HTTP_PORT`.

## Запуск тестов
В тестах требуется mongodb 4.0 (replica set). По умолчанию используется `localhost:27017/test?replicaSet=local`. Параметрами подключения можно управлять через переменные окружения:
- `JOB_QUEUE_USERNAME`
- `JOB_QUEUE_PASSWORD`
- `JOB_QUEUE_HOSTNAME`
- `JOB_QUEUE_DATABASE`
- `JOB_QUEUE_REPLICA_SET`

Если не хочется ставить локально, можно запускать в контейнере:
```bash
docker run --name mongo -d -p 27017:27017 mongo:4.0 --replSet local
docker exec -it mongo mongo --eval "rs.initiate({ _id: 'local', members: [{ _id: 0, host: '127.0.0.1:27017' }] })"
```

Standalone mongo недостаточно, так как используются транзакции.

## Ручное тестирование

* [Как протестировать изменения](./how-to-test.md)
* [Как протестировать изменения в Arcanum](./how-to-test-in-arcanum.md)

## Как протестировать изменения в Sandbox-тасках

1. Сделать ревью-реквест с изменениями в Sandbox-тасках.
2. Дождаться сборки тестового бинаря.

<img src="https://jing.yandex-team.ru/files/yuu-mao/Screen%20Shot%202021-07-06%20at%203.29.46%20PM.png" width="700">

<img src="https://jing.yandex-team.ru/files/yuu-mao/Screen%20Shot%202021-07-06%20at%203.33.18%20PM.png" width="700">

3. Подставить его `id` в [запуск](https://a.yandex-team.ru/arc_vcs/frontend/projects/microservices/services/merge-queue/modules/sandbox-utils.js?rev=r8380588#L221-246) задачи MQ:
```javascript
   const mqTaskParams = mergeConfigs([
        taskConfig,
        {
            tasks_archive_resource: 2265982632, // id ресурса SANDBOX_TASKS_BINARY
            description: `Resource 2265982632 test: ${getMergeQueueTaskDescription(prsToMerge, owner, repo)}`,
            custom_fields: [
                { name: 'project_github_owner', value: owner },
                { name: 'project_github_repo', value: repo },
                { name: 'pull_request_number', value: prNumber },
                { name: 'pull_request_provider', value: prProvider },
                { name: 'pull_request_merge_provider', value: prMergeProvider },
                { name: 'pull_request_head_commit', value: prHeadSha },
                { name: 'author_name', value: mergeAuthorLogin },
                { name: 'author_email', value: emailFromLogin(mergeAuthorLogin) },
                { name: 'config', value: JSON.stringify(mqConfig) },
                { name: 'webhook_urls', value: `${mqOrigin}/v2/sandbox/task` },
                {
                    name: 'refs_to_merge',
                    value: formatRefsToMerge(prsToMerge)
                },
                { name: 'success_build_uuid', value: trendboxUuid || '' },
                { name: 'success_build_task_id', value: buildId || '' },
                { name: 'should_skip_rebase_and_check', value: Boolean(buildId || trendboxUuid) },
                { name: 'node_js_version', value: '12' }
            ]
        }
    ]);
```

4. Протестировать изменения в GitHub/Arcanum.
