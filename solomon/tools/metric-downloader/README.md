## Build

```bash
$ ya make
```

Also need built **spack** tool for conversion

```bash
$ ya make ../spack/
```

## Download metrics

```bash
$ ./metric-downloader download solomon/solomon_gateway_spack
```

Command can download metrics from specified target in shard. By default, downloading from
preprod (https://solomon-pre.yandex-team.ru). Converting metrics to **application/x-solomon-txt** format and applying
selector.

## Requirements

1) available **ssh** to host solomon-dev-myt-00.search.yandex.net. Metric downloading processed by dev host.
2) available **scp** for downloading results from dev host.
3) built **spack** tool for metric conversion, spack must be in PATH variable.

## Supported metrics format

Can download only:

1) application/json
2) application/x-solomon-txt
3) application/x-solomon-spack
4) text/plain

**application/x-solomon-pb NOT supported**

## Syntax

Download metrics from one of pre (https://solomon-pre.yandex-team.ru) shards by default.
```bash
download <target> [<selector>]
```
Where < selector> can be empty or metrics selector

Where < target> can be:

1) project id: {{projectId}}. In that case you will choose needed shard and get metrics from random target in shard
     ```bash
       $ metric-downloader download solomon
     ```
2) project id and shard id: {{projectId}}/{{shardId}}. You get metrics from random target in shard
     ```bash
       $ metric-downloader download solomon/solomon_pre_coremon_spack
     ```
3) project id and shard id and target id: {{projectId}}/{{shardId}}/{{targetId}}. You get metrics from specified target
   in shard
     ```bash
       $ metric-downloader download solomon/solomon_pre_coremon_spack/pre-fetcher-man-007.mon.yandex.net
     ```
4) fully qualified id: {{env}}://{{projectId}}/{{shardId}}/{{targetId}}
     ```bash
       $ metric-downloader download pre://solomon/solomon_pre_coremon_spack/pre-fetcher-man-007.mon.yandex.net
     ```
   Available env: cloud_pre, cloud_prod, test, pre, prod.
5) metrics url: {{url}}
     ```bash
       $ metric-downloader download http://pre-alerting-sas-00.mon.yandex.net:4530/metrics/alertsStatus
     ```
6) with selector
     ```bash
         $ metric-downloader download http://sts1-iva-0000.mon.yandex.net:4550/metrics 'host="", type=="total"'
     ```
7) shard url
     ```bash
         $ metric-downloader download https://solomon.cloud.yandex-team.ru/admin/projects/solomon/shards/solomon_cloud_noc_agent
     ```
## Auth

Supports:

1) OAuth by variable **OAUTH_TOKEN**
2) IAM by secret path in variables **IAM_SECRET_FROM**. Example path = sec-01esbrr667re3f3jpmr8yh8hrr/gateway
