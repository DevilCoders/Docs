## Как писать свои правила

1. Напишите правило разбора в [infratest/services/zeroline/src/lib/resolution-rules](../../src/lib/resolution-rules).
2. Закиньте его в список правил - для [MQ-тикетов](../../src/lib/investigate/investigate-mq.ts), либо для [Infraduty-тикетов](../../src/lib/investigate/investigate-infraduty.ts).
3. Напишите свой анализатор в [infratest/packages/coroner/src/analysers](../../../../packages/coroner/src/analysers), по аналогии с существующими, пишите тест на анализатор, чтобы убедиться, что он выгребает нужные зацепки. Почитайте документацию [coroner](../../../../packages/coroner), он довольно просто устроен.
4. Не забудьте добавить его в [реестр анализаторов](../../../../packages/coroner/src/analysers/index.ts).
5. Не забудьте поднять [zeroline](../../#разработка) локально и протестировать интересующий вас тикет/таску:
   - для startrek-тикетов:
   ```(bash)
   curl -X POST http://localhost:3000/api/v1/investigate --data '{"issueKey":"MQ-123"}'
   ```
   - для sandbox-задач:
   ```(bash)
   curl -X POST http://localhost:3000/api/v1/report-task-status -d '{ "task_id": "1", "build_id": "3", "task_type": "SANDBOX_CI_WEB4", "project": "web4", "build_context": "pull-request", "status": "FAILURE", "duration": "1"}'
   ```
   В логах локально поднятого сервиса можно увидеть результат обработки запроса - следует убедиться, что новое правило применилось.
6. После влития пулреквеста с вашими изменениями [выпустите релиз](../how-to-release/how-to-release.md).

Вот пример ревью-реквеста с добавлением нового анализатора и правила разбора: https://a.yandex-team.ru/review/1477297/details
