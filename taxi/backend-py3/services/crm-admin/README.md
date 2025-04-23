crm-admin
===

# Spark

- [pyspark](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql.html)
- [SPYT docs](https://wiki.yandex-team.ru/spyt/)
- [SPYT queue](https://st.yandex-team.ru/SPYT/order:updated:true/filter?resolution=empty())

To restart the spark cluster follow the following steps

```bash
$ # https://github.yandex-team.ru/mnozdrachev/crm-admin-spark
$ git clone git@github.yandex-team.ru:mnozdrachev/crm-admin-spark.git
$ cd crm-admin-spark
$ python3.7 -mvenv venv
$ source ./venv/bin/activate
$ pip install -i https://pypi.yandex-team.ru/simple yandex-spyt

$ export ROBOT_CRM_YT_TOKEN=<token>

$ # find the currently running operation and stop it
$ yt --proxy=hahn list-operations --user=robot-crm-admin --pool=taxi-crm | grep '"id"'
$ yt --proxy=hahn abort-op <id>

$ ./launch.sh

$ deactivate
```

## UI

All actual endpoints can be found in spark discovery_path directory
(`//home/taxi-crm/production/spark/discovery`)

* `discovery/operation` - YT operation id
* `discovery/webui` - spark master WebUI address
* `discovery/shs` - spark history server address
* `discovery/rest` - spark REST API endpoint

## Spark jobs tests

There are also some tests for spark-jobs in
[crm-admin-spark](https://github.yandex-team.ru/mnozdrachev/crm-admin-spark).
Just install requirements (requirements.txt) and run pytest.

## TODO

Some tickets that might be useful
  * spark tests on yt-local <br>
    https://st.yandex-team.ru/SPYT-67

  * working links in spark history server UI <br>
    https://st.yandex-team.ru/SPYT-157

  * overwrite input table (we do not need a separte output table name for
    `spark_jobs/grouping.py` anymore) <br>
    https://st.yandex-team.ru/SPYT-157

  * respect `JAVA_PATH` in `java_gateway()` <br>
    https://st.yandex-team.ru/SPYT-165


# Quicksegment

[here](quicksegment.md)


# Grafana

* [Spark Metrics](https://grafana.yandex-team.ru/d/G_NaAzknk/crmadmin-spark-metrics?orgId=1)
* [YT Resources Usage](https://grafana.yandex-team.ru/d/Y2jf56VMz/crmadmin-yt-resources-usage?orgId=1)
