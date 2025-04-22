## Build

```bash
$ ya make
```

## Copy service dashboard

```bash
$ ./service-dashboard copy biiheb7ibas09sks01d6 fbeo9mfuup35slorffvu
```
Command can copy service dashboard from one environment to another.
By default, copy from preprod cloud(https://solomon.cloud-preprod.yandex-team.ru) to prod cloud(https://solomon.cloud.yandex-team.ru).
Previous version of dashboard will be pasted to https://paste.yandex-team.ru.

## Syntax
```bash
$ ./service-dashboard copy [flags] <from> <to>
```

where <from> and <to> can be:
1) dashboard ids {{id}
   Example:
   ```bash
   $ service-dashboard copy biiheb7ibas09sks01d6 fbeo9mfuup35slorffvu
   ```

2) fully qualified dashboard id: {{env}}://{{id}}
   Example:
   ```bash
   $ service-dashboard copy cloud_pre://biiheb7ibas09sks01d6 cloud_prod://fbeo9mfuup35slorffvu
   ```

Available env: cloud_pre, cloud_prod, test, pre, prod


## Auth

Supports:
1) OAuth by variable **OAUTH_TOKEN**
2) IAM by secret path in variables **IAM_SECRET_FROM** and **IAM_SECRET_TO**.
   Example path = sec-01esbrr667re3f3jpmr8yh8hrr/gateway
