###Модуль для разработки DQ компонентов

Генерация IDE проекта:
```shell
ya ide idea --with-content-root-modules --local --group-modules=tree --iml-in-project-root --ascetic --directory-based -r /Users/sbye/IdeaProjects/$(basename $(pwd)) .
```

Запуск Spark

prod:
```shell
spark-launch-yt --proxy hahn --discovery-path //home/market/production/mbo/mdm/dq/spyt --abort-existing --enable-advanced-event-log --worker-num 20 --worker-cores 8 --worker-memory 70G --pool market-production-mbo-mdm-dq --operation-alias market-production-mbo-mdm-dq-spark --master-memory-limit 8G --history-server-memory-limit 8G --tmpfs-limit 40G --spark-cluster-version 1.41.0
```

testing:
```shell
spark-launch-yt --proxy hahn --discovery-path //home/market/testing/mbo/mdm/dq/spyt --abort-existing --enable-advanced-event-log --worker-num 15 --worker-cores 8 --worker-memory 70G --pool market-testing-mbo-mdm-dq --operation-alias market-testing-mbo-mdm-dq-spark --master-memory-limit 8G --history-server-memory-limit 8G --tmpfs-limit 40G --spark-cluster-version 1.41.0
```
