Start from scratch:
=====================
1. Install [ycp](https://wiki.yandex-team.ru/cloud/devel/platform-team/dev/ycp/#install)
```bash
ycp components update && ycp init
```
2. Install [terraform](https://cloud.yandex.ru/docs/tutorials/infrastructure-management/terraform-quickstart)
3. Setup [mirror for terraform](https://clubs.at.yandex-team.ru/ycp/4790/4792)
4. Check [s3 writer role](https://abc.yandex-team.ru/services/solomon-cloud?scope=manage_store_systems)
   * the effect of a new role could be delayed for 5min or more
5. Create access key for [state storage](https://s3-idm.mds.yandex.net/stats/buckets/yc-solomon)
   * Get OAuth token from [link](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6797456f343042aabba07f49b478c49b)
   * List previously created access keys
   ```bash
   curl -qs -X POST -H "Authorization: OAuth $S3_OAUTH_TOKEN" "https://s3-idm.mds.yandex.net/credentials/list-access-keys" --data "service_id=3047" | json_pp
   ```
   * Remove unused keys
   ```bash
   curl -qs -X POST -H "Authorization: OAuth $S3_OAUTH_TOKEN" "https://s3-idm.mds.yandex.net/credentials/delete-access-key" --data "service_id=3047" --data "access_key_id=$ACCESS_KEY_ID"
   ```
   * Create new access key
   ```bash
   curl -qs -X POST -H "Authorization: OAuth $S3_OAUTH_TOKEN" "https://s3-idm.mds.yandex.net/credentials/create-access-key" --data "service_id=3047" --data "role=writer"
   ```
   * More information about [s3-api]((https://wiki.yandex-team.ru/mds/s3-api/authorization/))
6. Setup access key and secret to [state.tf file]
```
terraform {
    backend "s3" {
        endpoint = "s3.mds.yandex.net"
        bucket = "yc-solomon"
        key = "terraform/preprod/solomon.tfstate"
        region = "us-east-1"
        access_key = "XXX"
        secret_key = "XXX"
        skip_credentials_validation = true
        skip_metadata_api_check = true
    }
}
```
7. Initialize terraform configuration
```bash
terraform init
```
8. Check that everything is configured OK
```bash
terraform plan
```

Update Solomon stand:
=====================

  **Useful links: https://st.yandex-team.ru/SOLOMON-8253#620a85e3638504003cebfe8b**
- Create and transfer images at https://teamcity.aw.cloud.yandex.net/project/YDB_Solomon?mode=builds&showRootCauses=false
- Continue from the "Set variables" step at the **Setup for Solomon stand** procedure


Setup for Solomon stand:
========================

- Create overlay networks
  ```
  ycp --profile preprod vpc subnet update -e
  ```
- DNS Zone created in `bb://bootstrap-templates/terraform/<STAND>/monitoring` + `bb://bootstrap-templates/terraform/modules/monitoring`
- Create addresses for balancers:
  create yandex_only ipv6 for monitoring.yandexcloud.co.il (1)
  `ycp --profile preprod vpc address create -r qwe.yaml`

  `cat qwe.yaml`:

  ```
  name: "monitoring-yandexcloud-co-il-address"
  folder_id: "yc.monitoring.gateway"
  labels: {}
  ipv6_address_spec:
    requirements:
      hints:
      - yandex-only
  ```

  create yandex_only ipv6 for pm.mon.yandexcloud.co.il (3)
  `ycp --profile preprod vpc address create -r qwe.yaml`

  `cat qwe.yaml`:

  ```
  name: "pm-mon-yandexcloud-co-il-address"
  folder_id: "yc.monitoring.pm"
  labels: {}
  ipv6_address_spec:
    requirements:
      hints:
      - yandex-only
  ```

  create yandex_only = false ipv6 for monitoring.api.cloudil.com (2)
  `ycp --profile preprod vpc address create -r qwe.yaml`

  `cat qwe.yaml`:

  ```
  name: "monitoring-api-cloudil-com-address"
  folder_id: "yc.monitoring.gateway"
  labels: {}
  ipv6_address_spec:
    requirements: {}
  ```

  create yandex_only = false ipv4 for monitoring.api.cloudil.com (2)
  `ycp --profile preprod vpc address create -r qwe.yaml`

  `cat qwe.yaml`:

  ```
  name: "monitoring-api-cloudil-com-address-v4"
  folder_id: "yc.monitoring.gateway"
  labels: {}
  external_ipv4_address_spec:
    zone_id: il1-a
    region_id: il1
    requirements: {}
  ```

- Request DNS records:
  ```
  (bootstrap)
  monitoring.yandexcloud.co.il AAAA 2a11:f740:1:1::145  +PTR
  monitoring.private-api.yandexcloud.co.il CNAME monitoring.yandexcloud.co.il
  solomon.yandexcloud.co.il CNAME monitoring.yandexcloud.co.il

  (api-gateway)
  monitoring.api.cloudil.com AAAA 2a11:f740:2:1::2e7  +PTR
  monitoring.api.cloudil.com A 46.243.144.222  +PTR
  ```
- Set DNS records:
  `cp --profile preprod dns v1 dns-zone update-record-sets -r qwe.yaml`

  `cat qwe.yaml`:
  ```
  deletions: []
  dns_zone_id: "yc.bootstrap.monitoring"
  additions:
    - name: pm.mon.yandexcloud.co.il.
      type: AAAA
      ttl: "600"
      data:
      - 2a11:f740:1:1::98
      ui_protected: true
  ```
- Set packages
- Create networks, privileged update:
  `ycp --profile esrael vpc subnet update -r q.yaml`

  `cat q.yaml`:

  ```
  extra_params:
    hbf_enabled: false
    rpf_enabled: false
    export_rts: ["65533:666"]
    import_rts: ["65533:776"]
  labels: {}
  subnet_id: ddkttvnb289ggppk2euc
  update_mask:
    paths: [extra_params.import_rts, extra_params.export_rts]
  ```
  or move subnets creation to bb and get subnet_ids from `ycp --profile preprod vpc subnet list`

- Create images, create secrets
  https://wiki.yandex-team.ru/cloud/devel/platform-team/infra/skm/#source

  ```
  YC_TOKEN=$(ycp --profile preprod iam create-token) skm init skm.conf --kms-key-id <ID> --iam-private-endpoint iam.private-api.yandexcloud.co.il:14283 --kms-private-endpoint dpl.kms.private-api.yandexcloud.co.il:8443
  YC_TOKEN=$(ycp --profile preprod iam create-token) YAV_TOKEN=$(cat /.config/yav/.token) skm encrypt-md --config skm.conf | awk 'sub(/^    /, "")' > skm.yaml
  ```

- Transfer images
- Set variables
- Set s3 keys (for state storage, `curl https://s3-idm.mds.yandex.net/stats/buckets/yc-solomon`)
  https://wiki.yandex-team.ru/mds/s3-api/authorization/#sozdanieaccesskey (в idm должны быть соответствующие права - `S3 Writer` или `S3 Admin`):
  Запросы по работе с access keys аутентифицируются с помощью OAuth токена:
  https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6797456f343042aabba07f49b478c49b

  смотрим на список выписанных ключей в yc-solomon:
  `curl -qs -X POST -H "Authorization: OAuth $OAUTH" "https://s3-idm.mds.yandex.net/credentials/list-access-keys" --data "service_id=3047" | json_pp`
  удаляем лишнее:
  `curl -qs -X POST -H "Authorization: OAuth $OAUTH" "https://s3-idm.mds.yandex.net/credentials/delete-access-key" --data "service_id=3047" --data "access_key_id=0uh8BCB1L59h8u2LPcKN"`
  создаём новый ключ, если нужно (c ролью):
  `curl -qs -X POST -H "Authorization: OAuth $OAUTH" "https://s3-idm.mds.yandex.net/credentials/create-access-key" --data "service_id=3047" --data "role=writer"`

- Set state.tf (+ check https://clubs.at.yandex-team.ru/ycp/4790/4792)
- `terraform init`
- `terraform apply --parallelism=1`
- Create YDB database stuctures. Dump && restore

  `ydb -e grpcs://solomon-dn.ydb.cloud.yandex.net:2136 -d /global/solomon --sa-key-file ydb_global_iam.json --iam-endpoint iam.api.cloud.yandex.net tools dump --scheme-only -o crossdc_db`

  `ydb -e grpc://solomon-stockpile-sas-10.svc.cloud.yandex.net:2135 -d /sas/solomon tools dump --scheme-only -o az_db`

  `ydb.priv -v -e grpcs://u-lb.solomon.ydb.yandexcloud.co.il:2135 -d /preprod_global/solomon --iam-endpoint ts.private-api.yandexcloud.co.il:14282 --sa-key-file /Berkanavt/keys/solomon/ydb_global_iam.json tools restore ....`

  KV:

  `./kikimr -s grpc://u-lb.solomon-m1a.ydb.yandexcloud.co.il:2135 -f ydb.token db schema execute 'ModifyScheme { WorkingDir: "/preprod_m1a/solomon/Stockpile" OperationType: ESchemeOpCreateSolomonVolume CreateSolomonVolume { Name: "KV" ChannelProfileId: 0 PartitionCount: 4096 } }'`


Полезное:
========

  **Возможное упрощение для skm_*.yaml**

  ```
  echo '{"default_cert_id": "b2551m9q88271398fine", "monitoring_api_cert_id": "b25cmu2879cvc8sf294q", "monitoring_private_api_cert_id": "b25cmu2879cvc8sf294q"}' | \
  ./files/skm_generator.py -c skm_test.conf -k c42nc82uin2g2vebgmj5 -y ~/.config/yav/.token -e preprod --iam iam.private-api.yandexcloud.co.il:14283 --kms dpl.kms.private-api.yandexcloud.co.il:8443 --cert dpl.ycm.private-api.yandexcloud.co.il:8443 --lock cpl.lockbox.private-api.yandexcloud.co.il:8443 > skm_gateway.yaml
  ```

  `cat skm_test.conf`:

  ```
  /etc/nginx/ssl/default_cert.pem					0:0		440	certificate_manager://${default_cert_id}/certificate_chain
  /etc/nginx/ssl/default_key.pem					0:0		440	certificate_manager://${default_cert_id}/private_key
  /etc/nginx/ssl/monitoring_api_cert.pem				0:0		440	certificate_manager://${monitoring_api_cert_id}/certificate_chain
  /etc/nginx/ssl/monitoring_api_key.pem				0:0		440	certificate_manager://${monitoring_api_cert_id}/private_key
  /etc/nginx/ssl/monitoring_private_api_cert.pem			0:0		440	certificate_manager://${monitoring_private_api_cert_id}/certificate_chain
  /etc/nginx/ssl/monitoring_private_api_key.pem			0:0		440	certificate_manager://${monitoring_private_api_cert_id}/private_key
  /Berkanavt/keys/solomon/ydb_global_iam.pem			0:1800  	440	yav://sec-01fy9ta3zmd24aqpr00f85z6yy/yc.monitoring.ydb-sa.pem
  /Berkanavt/keys/solomon/iam.pem					0:1800		440	yav://sec-01fy9ta3zmd24aqpr00f85z6yy/yc.monitoring.gateway-sa.pem
  /Berkanavt/solomon/secrets/gateway_lb_producer_key.secret	1515:1515	440	yav://sec-01fy9ta3zmd24aqpr00f85z6yy/yc.monitoring.gateway-sa.json
  /Berkanavt/solomon/secrets/gateway.secrets			1800:1800	440	yav://sec-01fy9ta3zmd24aqpr00f85z6yy/gateway.secrets
  /Berkanavt/solomon/secrets/lb_jwt.secret			1515:1515	440	yav://sec-01fy9ta3zmd24aqpr00f85z6yy/yc.monitoring.gateway-sa.json
  ```

  **Скрипт для создания ключей для SA**

  ```
  #!/bin/sh

  SA="yc.monitoring.XXX-sa"

  openssl genrsa -out ${SA}.pem 4096
  openssl rsa -in ${SA}.pem -pubout > ${SA}.pub
  openssl pkcs8 -topk8 -nocrypt -in ${SA}.pem > ${SA}.priv

  awk -vsa=${SA} 'BEGIN {
          RS=""

          getline pub  < (sa ".pub");  gsub(/\n/, "\\n", pub)
          getline priv < (sa ".priv"); gsub(/\n/, "\\n", priv)

          print("{\"id\": \"" sa "-key\", \"service_account_id\": \"" sa "\", \"public_key\": \""pub"\", \"private_key\": \""priv"\"}")
  }' > ${SA}.json

  chmod 600 ${SA}.pem ${SA}.json
  ```
