# yc serverless trigger create cloud-logs

Create cloud logs trigger

#### Command Usage

Syntax: 

`yc serverless trigger create cloud-logs <TRIGGER-NAME> [Flags...] [Global Flags...]`

#### Flags

| Flag | Description |
|----|----|
|`--name`|<b>`string`</b><br/>Trigger name.|
|`--description`|<b>`string`</b><br/>Trigger description.|
|`--labels`|<b>`key=value[,key=value...]`</b><br/>A list of label KEY=VALUE pairs to add.|
|`--log-groups`|<b>`value[,value]`</b><br/>List of log groups to subscribe. A list can be specified by listing log groups separated by commas as well as passing this flag multiple times.<br/>|
|`--batch-size`|<b>`int`</b><br/>Batch size, 1 - 100. Default: 1|
|`--batch-cutoff`|<b>`duration`</b><br/>Batch cutoff. 1 - 60s. Default: 1s.|
|`--invoke-function-id`|<b>`string`</b><br/>Function to be invoked by worker on the data from Cloud Logs.|
|`--invoke-function-name`|<b>`string`</b><br/>Function to be invoked by worker on the data from Cloud Logs.|
|`--invoke-function-tag`|<b>`string`</b><br/>Function tag.|
|`--invoke-function-service-account-id`|<b>`string`</b><br/>Service account to be used by the worker to invoke the function.|
|`--invoke-function-service-account-name`|<b>`string`</b><br/>Service account to be used by the worker to invoke the function.|
|`--invoke-container-id`|<b>`string`</b><br/>Container to be invoked by worker on the data from Cloud Logs.|
|`--invoke-container-name`|<b>`string`</b><br/>Container to be invoked by worker on the data from Cloud Logs.|
|`--invoke-container-path`|<b>`string`</b><br/>Container endpoint path.|
|`--invoke-container-service-account-id`|<b>`string`</b><br/>Service account to be used by the worker to invoke the container.|
|`--invoke-container-service-account-name`|<b>`string`</b><br/>Service account to be used by the worker to invoke the container.|
|`--retry-attempts`|<b>`int`</b><br/>Retry attempts, Default: 0|
|`--retry-interval`|<b>`duration`</b><br/>Retry interval. Examples: '10s', '1m'.|
|`--dlq-queue-id`|<b>`string`</b><br/>Dead letter queue identifier.|
|`--dlq-service-account-id`|<b>`string`</b><br/>Service account to handle dead letter queue.|
|`--dlq-service-account-name`|<b>`string`</b><br/>Service account to handle dead letter queue.|
|`--async`|Display information about the operation in progress, without waiting for the operation to complete.|

#### Global Flags

| Flag | Description |
|----|----|
|`--profile`|<b>`string`</b><br/>Set the custom configuration file.|
|`--debug`|Debug logging.|
|`--debug-grpc`|Debug gRPC logging. Very verbose, used for debugging connection problems.|
|`--no-user-output`|Disable printing user intended output to stderr.|
|`--retry`|<b>`int`</b><br/>Enable gRPC retries. By default, retries are enabled with maximum 5 attempts.<br/>Pass 0 to disable retries. Pass any negative value for infinite retries.<br/>Even infinite retries are capped with 2 minutes timeout.|
|`--cloud-id`|<b>`string`</b><br/>Set the ID of the cloud to use.|
|`--folder-id`|<b>`string`</b><br/>Set the ID of the folder to use.|
|`--folder-name`|<b>`string`</b><br/>Set the name of the folder to use (will be resolved to id).|
|`--endpoint`|<b>`string`</b><br/>Set the Cloud API endpoint (host:port).|
|`--token`|<b>`string`</b><br/>Set the OAuth token to use.|
|`--format`|<b>`string`</b><br/>Set the output format: text (default), yaml, json, json-rest.|
|`-h`,`--help`|Display help for the command.|
