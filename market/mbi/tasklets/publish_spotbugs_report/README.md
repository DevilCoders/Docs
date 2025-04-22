`publish_spotbugs_report.py` - скрипт для анализа и публикации отчета spotbugs.
Используется в CI для проектов MBI в тасклетах `run_command` как ресурс из sandbox.

TODO: перенести код из скрипта `publish_spotbugs_report.py` в тасклет `publish_spotbugs_report`ю

## How to build and run

Собрать и запустить
```shell script
ya make
./publish_spotbugs_report run PublishSpotbugsReport --input "`cat input.json`" --local
```
Просмотр логов
```shell script
cat ~/.sandbox/logs/last_tasklet_run.log
```

Деплой(linux)
```shell script
ya make
./publish_spotbugs_report/publish_spotbugs_report sb-upload --sb-schema
```

Деплой(mac os)
```shell script
ya make --target-platform=linux
scp ./publish_spotbugs_report/publish_spotbugs_report {user}@braavos.market.yandex.net:/home/{user}/
ssh braavos.market.yandex.net
./publish_spotbugs_report sb-upload --sb-schema
```

