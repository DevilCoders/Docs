Quick start to read solomon backups:
=====================
1. Check [s3 reader role](https://abc.yandex-team.ru/services/solomon?scope=manage_store_systems)
   * the effect of a new role could be delayed for 5min or more
2. Create access key for [state storage](https://s3-idm.mds.yandex.net/stats/buckets/solomon-backup)
   * Get OAuth token from the [link](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6797456f343042aabba07f49b478c49b)
   * List previously created access keys
    ```bash
    curl -qs -X POST -H "Authorization: OAuth $S3_OAUTH_TOKEN" "https://s3-idm.mds.yandex.net/credentials/list-access-keys" --data "service_id=700" | json_pp
    ```
   * Remove unused keys
    ```bash
    curl -qs -X POST -H "Authorization: OAuth $S3_OAUTH_TOKEN" "https://s3-idm.mds.yandex.net/credentials/delete-access-key" --data "service_id=700" --data "access_key_id=$ACCESS_KEY_ID"
    ```
   * Create new access key
    ```bash
    curl -qs -X POST -H "Authorization: OAuth $S3_OAUTH_TOKEN" "https://s3-idm.mds.yandex.net/credentials/create-access-key" --data "service_id=700" --data "role=reader"
    ```
   * More information about [s3-api]((https://wiki.yandex-team.ru/mds/s3-api/authorization/))
3. Some usage examples (`{-b|--s3-bucket} BUCKET` - by default `solomon-backup` bucket is used):
   * List all backup prefixes:
    ```bash
    ./kv s3ls --key-file ~/.mds/keys --s3-enpoint s3.mds.yandex.net --prefix ""
    ```
   * List metadata (configs) backup for prod:
    ```bash
    ./kv s3ls --key-file ~/.mds/keys --s3-enpoint s3.mds.yandex.net --prefix prod/gateway
    ```
   * Download backup file:
    ```bash
    ./kv s3read --key-file ~/.mds/keys --s3-enpoint s3.mds.yandex.net --balancer-bypass prod/gateway/2022-05-25_20/Solomon/Config/V2/Dashboard.tgz ~/Dashboard.tgz
    ```

