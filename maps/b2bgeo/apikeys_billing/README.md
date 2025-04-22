### Sandbox
**Code of Sandbox tasks**
\
arcadia/sandbox/projects/ApikeysB2bgeo/
\
https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/ApikeysB2bgeo/

**Upload binaries to sandbox**

`ya upload -d='apikeys_stat binary' -a='linux' --do-not-remove --token=$SANDBOX_TOKEN --ttl=inf -T=B2BGEO_APIKEYS_STAT_BIN apikeys_stat`

`ya upload -d='preprocess_geosaas_logs binary' -a='linux' --do-not-remove --token=$SANDBOX_TOKEN --ttl=inf -T=B2BGEO_PREPROCESS_GEOSAAS_LOGS_BIN preprocess_geosaas_logs`

`ya upload -d='check_failed_logs binary' -a='linux' --do-not-remove --token=$SANDBOX_TOKEN --ttl=inf -T=B2BGEO_CHECK_FAILED_LOGS_BIN check_failed_logs`

### Description and current settings of sandbox tasks
**preprocess_geosaas_logs**
\
By default, script takes tables from\
`hahn://home/logfeller/logs/saas-maps-access-log/stream/5min`\
and converts them to tables with same names in\
`hahn://home/b2bgeo/data/apikeys/processed_logs`\
Script takes latest table in `/stream/5min` which is not in `/processed_logs` yet; if no such tables, it exits.
No more than 1000 tables in `/processed_logs`, old tables are deleted.

Sandbox scheduler https://sandbox.yandex-team.ru/scheduler/7372/view \
Runs every 60 seconds; retry on failure in 120 seconds. Failure states are emailed to `b2bgeo-alerts@yandex-team.ru` \
Typical reason of failure: default YT cluster (Hahn) is unavailable. 

**push_apikeys_stat**

By default, script takes tables from\
`hahn://home/b2bgeo/data/apikeys/processed_logs`\
and pushes them line-by-line to APIKeys, writing results to corresponding table in\
`//home/b2bgeo/data/apikeys/stat`\
Script takes latest table in `/processed_logs`, but only if it is older than 22:30 Yesterday 
(thus, if old yesterdays' tables somehow were not processed, you'll need either to process them manually, taking into account,
that they will appear in today's statistics, or to drop them).\
Script sets attribute `apikeys_stat` for tables in `/processed_logs`:
- `started` when it starts pushing table to APIKeys
- `completed` if table is pushed and everything is OK
- `failed` if table is pushed and at least one record was not pushed for some reason (popular reason: key is invalid).

No more than 1000 tables in `/stat`, old tables are deleted.

Sandbox scheduler https://sandbox.yandex-team.ru/scheduler/7373/view \
Runs every 60 seconds; retry on failure in 120 seconds. Failure states are emailed to `b2bgeo-alerts@yandex-team.ru` \
Typical reason of failure: default YT cluster (Hahn) is unavailable. 

**check_failed_logs**

Script takes tables from\
`hahn://home/b2bgeo/data/apikeys/processed_logs` and `//home/b2bgeo/data/apikeys/stat`,\
analyzes them for potential problems and sends emails to `b2bgeo-alerts@yandex-team.ru`\
Types of problems:
1. "new failed tables": tables with attribute `apikeys_stat=failed` in `//home/b2bgeo/data/apikeys/stat` 
not copied to `//home/b2bgeo/data/apikeys/failed_logs`. 
Action: copy table from `/stat` and corresponding table from `/processed_logs`
to `/failed_logs`, send email with list of copied tables.
2. "tables in processed_logs_dir not pushed to APIKeys": some tables in `/processed_logs` older than 60 minutes were not pushed to APIKeys.
Possible reason: delay in YT or Sandbox or APIKeys. If table is from today, most probably it will be pushed later, so do nothing. 
If table is earlier than 22:30 yesterday, it will not be pushed by `push_apikeys_stat` script, in such case problem *should be resolved manually*, see Troubleshooting section.
3. "Missing tables (gaps) or extra tables in processed_logs_dir": some tables in `/processed_logs` do not satisfy 5min-log-interval pattern. 
Check manually. Had never seen such error yet.  

Sandbox scheduler https://sandbox.yandex-team.ru/scheduler/7711/view \
Runs every hour; retry on failure in 5 minutes.

### Troubleshooting
**check_failed_logs: "Found tables in processed_logs_dir not pushed to APIKeys and older than %s minutes"**
1. If table name is >=22:30 yesterday, just wait. Most probably, problems with YT/Sandbox will be fixed soon, and table will be pushed to APIKeys.
2. If table name is earlier than 22:30 yesterday, then look at table contents and make a decision.

2A. Number of cells/requests is insufficient (we don't loose much money). We don't want to push stats from the table manually. Set attribute to prevent new alerts from `check_failed_logs`: `yt set //home/b2bgeo/data/apikeys/processed_logs/2018-05-16T20:30:00/@apikeys_stat 'completed'`.

2B. Number of cells/requests is sufficient, we want to push data to APIKeys, even though it will appear in today's stats (APIKeys can not update yesterday's data). 
Go to sandbox.yandex-team.ru and create `YA_EXEC` task with the following parameters:
\
`Svn url for arcadia = arcadia:/arc/trunk/arcadia`
\
`Program to build and run = maps/b2bgeo/apikeys_billing/apikeys_stat/apikeys_stat`
\
`Args to program	= --mode table --table TABLE_NAME_FROM_PROCESSED_LOGS_DIR_NOT_FULL_PATH`
\
`Environment params = APIKEYS_ENV='production' YT_TOKEN='$(vault:value:B2BGEO:robot_b2bgeo_yt_token)'`
\
Or simply clone https://sandbox.yandex-team.ru/task/249736722/view if it still exists

2C. Just do nothing and wait until not-pushed table is pruned from `/processed_logs` dir (approx 3 days), recieving hourly emails from `check_failed_logs`.  

**check_failed_logs: "Last table ... is older than expected"**
1. Most probably, some delay in YT/Sandbox. Check yt-announces@, yt@ and sandbox@ mailing lists to see if clusters are not shot down.
2. Go to https://sandbox.yandex-team.ru/tasks and check execution time of recent tasks PREPROCESS_GEOSAAS_LOGS (typical time 1-5 min) and PUSH_APIKEYS_STAT (typical time < 3 min). Big execution time usually says about heavy load on YT clusters.

**check_failed_logs: "Found new failed tables and copied them to failed_logs dir"**
1. Go to `//home/b2bgeo/data/apikeys/failed_logs`, find tables from email. For every time interval there should be two tables: from `/processed_logs/` and from `/stat`.
2. Read contents of those tables, identify apikey having `cur_status=failed`, read `exceptions`.
3. Look up for apikey in APIKeys (ask managers with access to production APIKeys - dvshelehov@).
4. Case: apikey is not in APIKeys   
\
4A. Somebody is making requests to Geosaas-stable with incorrect apikey (not existing in APIKeys) from Yandex internal network. 
\
First, ask Geosaas team, are they testing something (they use keys like 'trololo' or write extra symbols to real apikeys).
\
If they say they don't do anything then grep corresponding log table: `yt map --format dsv --src //home/logfeller/logs/saas-maps-access-log/stream/5min/TABLE_NAME --dst //tmp/grep_results 'awk "/INCORRECT_APIKEY_HERE/"'`
\
Check 'ip' field. Find this IP in https://racktables.yandex-team.ru/ , sometimes it points to certain Yandex employee/team. 
\
4B. Same case, but ip is external. It means that Geosaas proxy protection against unregistered apikeys failed. Write to Geosaas team.  
5. Apikey is in APIKeys. Check `exceptions` field. Check tasks PUSH_APIKEYS_STAT, find the one where problem appeared (you'll have to read logs in several latest tasks, sorry) and check stderr.
If problem appeared as a result of APIKeys inavailability, write to APIKeys team.

### Testing
**How to test check_failed_logs**
\
Test failed log: make internal request to stable GeoSaas \
`curl 'http://saas-searchproxy-maps.yandex.net:17000/?service=default-router&ms=proto&hr=json&meta_search=first_found&sp_meta_search=aproxy&timeout=5000000&balancertimeout=2000&text=type:route_mn;d:100;perm:ptAuto;from:51.436507%2035.709166;to:51.459838%2035.715912&apikey=helloworld'`\
check_failed_logs should find log table with unprocessed apikey 'helloworld'\
\
Test unprocessed log: make a copy of some old table (older than yesterday evening) in processed_logs dir. Apikeys_stat will not push stat from this table< but check_failed_logs should find it and send an email.


### GeoSaas
**Server settings on GeoSaas side**
\
searchproxy.conf in https://nanny.yandex-team.ru/ui/#/services/catalog/saas_maps_b2b_proxy/files \
Current settings: https://paste.yandex-team.ru/341805




