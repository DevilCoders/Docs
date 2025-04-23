## Postgres to YT

1. Creation of source ([link](https://docs.yandex-team.ru/cloud/data-transfer/operations/prepare#source-pg))
    - Create new user so that users don't overlap. Each user has limit connection to database. You need to calculate how much you need to datatransfer replication. Let's say default is `5`
    - For generanting user password you can use `node -p "crypto.randomBytes(64).toString('base64').replace(/=/g, '')"`
    - Select cluster mdb and add tables for replication. For example, `public.history`
2. Creation of receiver
    - Select cluster and YT path for store data
    - For `copy and replicate` select dynamic tables in YT
    - Tablet cell bundle is `default` if you don't have own
    - Use HDD
    - Add permission for robot [robot-lf-dyn-push](https://staff.yandex-team.ru/robot-lf-dyn-push): read/write/delete/mount for your table
    - Add ACL for small scope if data has sensitive information
3. Creation of data transfer
    - Select source and receiver
    - Leave all default settings if you don't have other in mind
4. Add monitoring for delay with lama preset
    - [Preset](https://a.yandex-team.ru/arcadia/maps/analytics/tools/lama/presets/data_transfer/delay.jinja)
    - [Example](https://a.yandex-team.ru/arcadia/maps/front/services/parking-int/schedulers/lama.yaml)



### [Datatransfer docs](https://docs.yandex-team.ru/cloud/data-transfer)
