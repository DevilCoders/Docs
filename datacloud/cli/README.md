# CLI

Cli - это набор консольных утилит, облегчающих выполнение часто возникающих нерегулярных задач

На данный момент доступны следующие утилиты:
- [make_ready/apply_api_models](https://a.yandex-team.ru/arc/trunk/arcadia/datacloud/cli/make_ready/apply_api_models) -- примененить модель
- [make_ready/check_model_stability](https://a.yandex-team.ru/arc/trunk/arcadia/datacloud/cli/make_ready/check_model_stability) -- проверить стабильность модели
- [make_ready/transfer_score](https://a.yandex-team.ru/arc/trunk/arcadia/datacloud/cli/make_ready/transfer_score) -- загрузить таблицу сос кором на YDB
- [upload_model](https://a.yandex-team.ru/arc/trunk/arcadia/datacloud/cli/upload_model) -- раскатить новый бинарник модели в прод

## Важно помнить:
- Все утилиты из make_ready лишь выставляют нужную задачу в статус READY в [status_db](https://yt.yandex-team.ru/hahn/navigation?path=//home/x-products/production/new-status-db&offsetMode=key). Чтобы задача отработала, нужно либо дождаться пока ClusterMaster решит ее выполнить, либо запустить ее в графе вручную