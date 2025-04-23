###### Ссылки Testing

- [Рабочая директория в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/mbo/mdm/dq/spyt)
- [Spark операция в YT](https://yt.yandex-team.ru/hahn/operations?user=robot-mdm-dq-test&state=running)
- [Директория с результатами DQ проверок](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/mbo/mdm/dq/dq_result)
- [Подключение к БД DQ (Data mart)](https://yav.yandex-team.ru/secret/sec-01ezxzwn5945f224ksap9amph2/explore/versions)

###### Ссылки Production

- [Рабочая директория в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/mdm/dq/spyt)
- [Spark операция в YT](https://yt.yandex-team.ru/hahn/operations?user=robot-mdm-dq-prod&state=running)
- [Директория с результатами DQ проверок](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/mdm/dq/dq_result)
- [Подключение к БД DQ (Data mart)](https://yav.yandex-team.ru/secret/sec-01ezy04k560nx16vt3fa7fwe95/explore/versions)

###### Посмотреть лог выполнения проверок dq

```postgresql
select *
from sync.task_log
order by id desc;
```

###### Посмотреть на каком хосте какие источники проверок DQ выполняются в данный момент

```postgresql
select *
from sync.task;
```

###### Запуск Spark-а

Testing:
```shell
spark-launch-yt --proxy hahn --discovery-path //home/market/testing/mbo/mdm/dq/spyt --abort-existing --enable-advanced-event-log --worker-num 15 --worker-cores 8 --worker-memory 70G --pool market-testing-mbo-mdm-dq --operation-alias market-testing-mbo-mdm-dq-spark --master-memory-limit 8G --history-server-memory-limit 8G --tmpfs-limit 40G --spark-cluster-version 1.41.0
```

Production:
```shell
spark-launch-yt --proxy hahn --discovery-path //home/market/production/mbo/mdm/dq/spyt --abort-existing --enable-advanced-event-log --worker-num 20 --worker-cores 8 --worker-memory 70G --pool market-production-mbo-mdm-dq --operation-alias market-production-mbo-mdm-dq-spark --master-memory-limit 8G --history-server-memory-limit 8G --tmpfs-limit 40G --spark-cluster-version 1.41.0
```

{% note info "Note" %}

Скрипт для старта Spark-а лучше запускать из контейнера с DQ (зайти по SSH).
Параметр --spark-cluster-version 1.41.0 должен выбираться исходя из текущего SPYT слоя в контейнере.

{% endnote %}

###### Алгоритм релиза проверок от ДС
- Запустить ЦУМ [пайплайн](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/dq-pipelines)
- Выкатить на dev и test
- Отписаться в релизной таске (о выкате на тест)
- Ожидать подтверждения корректности работы проверок от ДС
- Вытить на prod
- Закрыть релизную таску
