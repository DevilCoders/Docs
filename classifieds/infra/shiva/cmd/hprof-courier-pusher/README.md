Hprof Courier Pusher
===

This service does next action:
- looks for new hprof dumps on docker hosts and uploads to S3;
- sends metadata about dumps to Hprof Courier API.

The service is supplied to hosts as Nomad's system job via jenkins:
https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/testing/job/hprof-courier-pusher/
https://j.vertis.yandex-team.ru/job/Deploys/job/Admins/job/production/job/hprof-courier-pusher/

