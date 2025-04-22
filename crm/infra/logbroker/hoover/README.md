# CRM Logbroker proxy to .NET services

Hoover reads messages from Logbroker and transmit them to specified API

## Environment variables

| Variable | Type | Default | Description | Example |
|:-------- |:----:|:-------:|:------------|:--------|
|`API_HANDLER_URL` | String | | target api endpoint | `https://crm.yandex-team.ru/ping` |
|`API_SEND_BATCHES` | Boolean | `false` | send event batches to api | |
|`API_BATCH_MAX_SIZE` | Int | 8192 | max size of one batch | |
|`API_IGNORE_HANDLER_ERRORS` | Boolean | `false` | Accept only 2xx answers from API or not | |
|`API_TVM_SRC_ALIAS` | String | `hoover` | Hoover alias in tvm client for API service tickets | |
|`API_TVM_DST_ALIAS` | String | `target` | API alias in tvm client | |
|`LOGBROKER_INSTALLATION` | String | `logbroker.yandex.net:2135` | Logbroker installation with port | |
|`LOGBROKER_DATABASE` | String | `/Root` | Logbroker database | |
|`LOGBROKER_TOPICS` | String | | Logbroker topics path. Delimiter - `;` | `/crm/events/stable/issues;/crm/events/prestable/issues` |
|`LOGBROKER_CONSUMER` | String | | Logbroker consumer path | `/crm/events/stable/consumer` |
|`LOGBROKER_TVM_SRC_ALIAS` | String | `hoover` | Hoover alias in tvm client for Logbroker service tickets | `klb` |
|`LOGBROKER_TVM_DST_ALIAS` | String | `logbroker` | Logbroker alias in tvm client | |

### For local development

| Variable | Type | Default | Description | Example |
|:-------- |:----:|:-------:|:------------|:--------|
|`DEPLOY_TVM_TOOL_URL` | String | | URL of running tvmtool | `localhost:18000` |
