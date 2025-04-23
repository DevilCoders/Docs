### What is this
Temporal has an official repo with "standard" Grafana dashboards: https://github.com/temporalio/dashboards

We adopted and adapted them for our needs.
This folder contains throw-away scripts that
* take the original dashboard definition downloaded from GitHub
* rewrite all the PromQL queries to SolomonQL, set data source to Solomon, etc
* upload the result to Grafana API


Token for communicating with Solomon and Grafana can be obtained from
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=aa78b151370f4b5aabf3882ad715d263
### Existing dashboards

* `./sdk.json`
Source: https://raw.githubusercontent.com/temporalio/dashboards/master/dashboards/sdk.json
Grafana: https://grafana.yandex-team.ru/d/WpTankt7k/temporal-awacs-worker?orgId=1
```sh
SOLOMON_PROJECT=swat-temporal \
SOLOMON_CLUSTER=awacs_worker \
SOLOMON_SERVICE=awacs_worker \
GRAFANA_DASHBOARD_UID=WpTankt7k \
TOKEN=AQAD-XXX python augment-sdk.py
```

* `frontend.json`
Source: https://raw.githubusercontent.com/temporalio/dashboards/master/dashboards/frontend.json
Grafana: https://grafana.yandex-team.ru/d/RolIS4t7z/temporal-frontend?orgId=1
```sh
SOLOMON_PROJECT=swat-temporal \
SOLOMON_CLUSTER=frontend \
SOLOMON_SERVICE=frontend \
GRAFANA_DASHBOARD_UID=RolIS4t7z \
TOKEN=AQAD-XXX python augment-frontend.py
```

### Related links
* https://st.yandex-team.ru/AWACS-1153
* SWAT Temporal Solomon project:
https://solomon.yandex-team.ru/admin/projects/swat-temporal
* List of Temporal metrics:
https://github.com/temporalio/temporal/blob/c24eaa4be8d3f3c50c954dea91ef81fa16623518/common/metrics/defs.go#L2525
* To test Solomon queries:
https://solomon.yandex-team.ru/admin/projects/swat-temporal/autoGraph
* To explore existing Solomon metrics:
https://monitoring.yandex-team.ru/projects/swat-temporal/explorer/queries?range=1h&q.0.s=%7Bproject%3D%22swat-temporal%22%2C%20service%3D%22awacs_worker%22%2C%20cluster%3D%22awacs_worker%22%2C%20name%3D%22temporal_temporal_workflow_failed%22%7D&refresh=60&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default
