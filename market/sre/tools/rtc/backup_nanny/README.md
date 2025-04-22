# backup-nanny
> A simple tool to create and upload backups of Nanny services

## How it works?
1. Gets list of Nanny service IDs by the login of one of the owners, i.e. `d3rp`.
2. Dumps the configurations of the services by their IDs to json files.
3. Adds the json files into a tarball.
4. Uploads the tarball via [Logkeeper](http://a.yandex-team.ru/arc/trunk/arcadia/market/sre/tools/logkeeper) to [S3](https://logs.market.yandex.net/sandbox).  

## Usage example
There are no command line arguments at that point because this tool is meant to be used as a scheduled Sandbox task.
```
> DEBUG=1 bin/backup-nanny
2018-11-07 14:08:19,600 root         DEBUG    Creating the backup of configurations of Nanny services (-1)
2018-11-07 14:08:19,662 sandbox.common.rest DEBUG    REST API client instance created in thread '4549223872' with oauth token authorization.
2018-11-07 14:08:20,095 backup       DEBUG    Creating a tarball "nanny-services-backup.2018-11-07.tar.gz"
2018-11-07 14:08:20,097 backup       DEBUG    Getting service "prod_market_light_matcher_sas"
2018-11-07 14:08:20,347 backup       DEBUG    Preparing tarinfo for "prod_market_light_matcher_sas.json"
2018-11-07 14:08:20,347 backup       DEBUG    Adding "prod_market_light_matcher_sas.json"
...
2018-11-07 14:10:45,879 backup       INFO     Added 883 files into nanny-services-backup.2018-11-07.tar.gz
2018-11-10 20:48:25,968 backup       DEBUG    Start uploading "nanny-services-backup.2018-11-10.tar.gz"
2018-11-10 20:48:25,968 backup       DEBUG    Uploading "nanny-services-backup.2018-11-10.tar.gz"
2018-11-10 20:48:25,968 market.sre.tools.logkeeper.core.log_helper DEBUG    Creating a new ApiClient
2018-11-10 20:48:25,969 market.sre.tools.logkeeper.core.api_client DEBUG    Request configs for minion: '{\n    "host": "sandbox",\n    "service": "backup-nanny"\n}'
2018-11-10 20:48:26,061 market.sre.tools.logkeeper.core.log_helper DEBUG    Setting S3 up
2018-11-10 20:48:26,062 s3           DEBUG    s3 connection would be done for host "s3.mds.yandex.net"
2018-11-10 20:48:26,062 s3           DEBUG    lookup bucket logkeeper
2018-11-10 20:48:26,124 s3           DEBUG    lookup bucket result: logkeeper
2018-11-10 20:48:26,124 market.sre.tools.logkeeper.core.log_helper DEBUG    LogHelper is prepared
2018-11-10 20:48:26,125 market.sre.tools.logkeeper.core.log_helper DEBUG    Pattern "nanny-services-backup.*.gz" matches the file path "nanny-services-backup.2018-11-10.tar.gz"
2018-11-10 20:48:26,125 market.sre.tools.logkeeper.core.api_client DEBUG    Register minion as ready to upload: '{\n    "status": "waiting",\n    "host": "sandbox",\n    "percent": "None",\n    "service": "backup-nanny",\n    "filename": "public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz"\n}'
2018-11-10 20:48:26,178 market.sre.tools.logkeeper.core.api_client DEBUG    Register minion as ready to upload: '{\n    "status": "waiting",\n    "host": "sandbox",\n    "percent": "None",\n    "service": "backup-nanny",\n    "filename": "public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz"\n}'
2018-11-10 20:48:26,221 market.sre.tools.logkeeper.core.log_helper DEBUG    Uploading file "nanny-services-backup.2018-11-10.tar.gz" to "public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz"
2018-11-10 20:48:26,222 market.sre.tools.logkeeper.core.api_client DEBUG    Register minion as ready to upload: '{\n    "status": "uploading",\n    "host": "sandbox",\n    "percent": "0",\n    "service": "backup-nanny",\n    "filename": "public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz"\n}'
2018-11-10 20:48:26,273 market.sre.tools.logkeeper.core.log_helper DEBUG    Destination key of the file is "public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz"
2018-11-10 20:48:26,308 s3           DEBUG    Upload part #1
2018-11-10 20:48:26,543 s3           DEBUG    Multipart upload complete. Uploaded 1229502 bytes by 1 chunks to path public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz
2018-11-10 20:48:26,605 market.sre.tools.logkeeper.core.log_helper DEBUG    File "nanny-services-backup.2018-11-10.tar.gz" is uploaded
2018-11-10 20:48:26,605 market.sre.tools.logkeeper.core.api_client DEBUG    Register minion as ready to upload: '{\n    "status": "archived",\n    "host": "sandbox",\n    "percent": "1229502",\n    "service": "backup-nanny",\n    "filename": "public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz"\n}'
2018-11-10 20:48:26,660 market.sre.tools.logkeeper.core.log_helper DEBUG    Registering the uploaded file public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz
2018-11-10 20:48:26,661 market.sre.tools.logkeeper.core.api_client DEBUG    Register the log file: '{\n    "tskv": false,\n    "mdate": "2018-11-10",\n    "baseDir": "/mfsroot/public",\n    "host": "sandbox",\n    "ttl": 31,\n    "group": "sandbox",\n    "fullPath": "public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-10.tar.gz",\n    "config": "backup-nanny",\n    "size": "1229502"\n}'
2018-11-10 20:48:26,702 backup       DEBUG    File "nanny-services-backup.2018-11-10.tar.gz" uploaded
2018-11-10 20:48:26,703 root         INFO     Backup has been created
> ls -la nanny-services-backup.2018-11-07.tar.gz
-rw-r--r-- 1 d3rp 787531 Nov  7 14:10 nanny-services-backup.2018-11-07.tar.gz
```
Nanny token is obtained via SSH, also it can be passed via an environment variable `NANNY_OAUTH_TOKEN`.

## Every day backups
Backups should be created every day so a Sandbox scheduler [task](https://sandbox.yandex-team.ru/scheduler/11835/view) has been added and configured for daily execution.

## How to restore the configuration of a service from backup?
Follow the steps:
1. Find a tarball link [here](http://logs.market.yandex.net/sandbox), i.e. https://logkeeper.market.yandex.net/get-file/public/nanny-services-backup/backup-nanny/sandbox/backup-nanny/nanny-services-backup.2018-11-14.tar.gz
2. Use [repl](market/sre/tools/rtc/rtc-repl)
  ```
  In [1]: url = ("https://logkeeper.market.yandex.net/get-file/public/nanny-services-backup/backup-nanny/sandbox/"
     ...:        "backup-nanny/nanny-services-backup.2018-11-14.tar.gz")

  In [2]: service = nanny.utils.load_from_backup(url=url, service_id="testing_market_front_desktop_sas")

  In [3]: service.id
  Out[1]: u'testing_market_front_desktop_sas'

  In [4]  # `service` is an instance of `Service` object, it can be changed, uploaded partially or as is
  ```

## TODO
- consumes too much memory, around 300-400MB

## Links

https://st.yandex-team.ru/CSADMIN-22640
