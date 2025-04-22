# jyggalag

Qloud-redeploy daemon/cli

## How to

### "Install"
```bash
cd arcadia; ya make --checkout -j0 infra/rtc/sbin/jyggalag; cd infra/rtc/sbin/jyggalag; ya make
echo "alias jyggalag='${PWD}/jyggalag'" >>~/.profile

# Optional for daemon
mkdir -p ~/.postgresql ; wget --no-check-certificate "https://crls.yandex.net/allCAs.pem" -O ~/.postgresql/root.crt ; chmod 0600 ~/.postgresql/root.crt
```

### Run
```bash
jyggalag --help
```

## Emergency Shut Down
Run script from:
https://yav.yandex-team.ru/secret/sec-01dghyd6dam36v46jp7cbb44zz/explore/versions
or
Deactivate Service
https://qloud.yandex-team.ru/projects/qloud/jyggalag/prod
YASM panel: https://yasm.yandex-team.ru/panel/jyggalag 

## Daemon config

jyggalag waits config in ```~/.jyggalag/config.json```
### Example
```json
{
  "pg_hosts": "host1,host2,host3",
  "pg_port": "6432",
  "pg_name": "jyggalag",
  "pg_login": "jyggalag",
  "pg_pass": "qwerty",
  "unistat_listen_host": "::",
  "unistat_listen_port": 8082,
  "walle_oauth": "AQAD-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
  "qloud_oauth": "AQAD-aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
  "qloud_redeploy_segments": ["qloud-ext.common", "qloud-ext.personal", "qloud-ext.outsource"],
  "qloud_redeploy_dcs": ["MAN", "MYT", "IVA", "SAS", "VLA"],
  "jyggalag_release_max_ops": 2,
  "jyggalag_release_timeout": 7200
}
```

## CLI commands for qloud hosts management
CLI requires ```qloud_oauth``` in config or ENV `
Optional  ```walle_oauth``` in config or ENV

### List Hosts
```bash
cat hosts_invs_or_names | ./jyggalag.py hosts-list
inv       name                        wproject qsegment       qstate wstate   wstatus qslots
102911554 sas2-7940.search.yandex.net qloud    qloud-ext.mail DOWN   assigned ready   0
102911560 sas2-7939.search.yandex.net qloud    qloud-ext.mail DOWN   assigned ready   0
102911561 sas2-7918.search.yandex.net qloud    qloud-ext.mail DOWN   assigned ready   0
```

#### Add hosts to qloud
```bash
cat hosts_invs_or_names | ./jyggalag.py hosts-add qloud-ext.segment_name
inv       name                        wproject qsegment               qstate  wstate   wstatus qslots
102911554 sas2-7940.search.yandex.net qloud    qloud-ext.segment_name INITIAL assigned ready   0
102911560 sas2-7939.search.yandex.net qloud    qloud-ext.segment_name INITIAL assigned ready   0
102911561 sas2-7918.search.yandex.net qloud    qloud-ext.segment_name INITIAL assigned ready   0
```

### Change HFSM state in qloud
```bash
cat hosts_invs_or_names | ./jyggalag.py hosts-state [UP|DOWN|...] --message 'ST'
inv       name                        wproject qsegment       qstate wstate   wstatus qslots
102911554 sas2-7940.search.yandex.net qloud    qloud-ext.mail DOWN   assigned ready   0
102911560 sas2-7939.search.yandex.net qloud    qloud-ext.mail DOWN   assigned ready   0
102911561 sas2-7918.search.yandex.net qloud    qloud-ext.mail DOWN   assigned ready   0
```

Also instead of hosts-state, you can use  ```hosts-up``` or ```hosts-down``` 

### Switch hosts segment in qloud
```bash
cat hosts_invs_or_names | ./jyggalag.py hosts-switch-segment qloud-ext.common --message 'ST'
inv       name                        wproject qsegment         qstate wstate   wstatus qslots
102911554 sas2-7940.search.yandex.net qloud    qloud-ext.common DOWN   assigned ready   0
102911560 sas2-7939.search.yandex.net qloud    qloud-ext.common DOWN   assigned ready   0
102911561 sas2-7918.search.yandex.net qloud    qloud-ext.common DOWN   assigned ready   0
```

### Update hosts meta from oops
```bash
cat hosts_invs_or_names | ./jyggalag.py hosts-meta
inv       name                        wproject qsegment         qstate  wstate   wstatus qslots
102911554 sas2-7940.search.yandex.net qloud    qloud-ext.common INITIAL assigned ready   0
102911560 sas2-7939.search.yandex.net qloud    qloud-ext.common INITIAL assigned ready   0
102911561 sas2-7918.search.yandex.net qloud    qloud-ext.common INITIAL assigned ready   0
```

### Remove hosts from qloud
```bash
cat hosts_invs_or_names | ./jyggalag.py hosts-remove
inv       name                        wproject qsegment qstate wstate   wstatus qslots
102911554 sas2-7940.search.yandex.net qloud    NULL     NULL   assigned ready   0
102911560 sas2-7939.search.yandex.net qloud    NULL     NULL   assigned ready   0
102911561 sas2-7918.search.yandex.net qloud    NULL     NULL   assigned ready   0
```

### List Services on hosts
```bash
cat hosts_invs_or_names | ./jyggalag.py hosts-services
14 qloud-ext.mail.akita.production
1 qloud-ext.mail.akita.prestable
```


## CLI commands for daemon
Requires posgresql data in config

### current status
```bash
./jyggalag.py daemon-list
```

### hosts that do not change status more than a day 
```bash
./jyggalag.py daemon-timeouts
```

### logs for the last week
```bash
./jyggalag.py daemon-lastlog
```

### hosts that waiting for ok to release
```bash
./jyggalag.py daemon-pending
```

### ok for pending hosts
```bash
cat hosts | ./jyggalag.py daemon-ok
```
or
```bash
./jyggalag.py daemon-ok --host iva2-blabla
```

## Hosts states

```
QLOUD_REDEPLOY_QUEUED           // Nothing to do
QLOUD_REDEPLOY_RELEASE_PENDING  // Host is SUSPECTED in Qloud, waiting for OK
QLOUD_REDEPLOY_RELEASING        // Host is DOWN in Qloud, waiting for services to disappear
QLOUD_REDEPLOY_ERASING          // Host becoming free/ready in wall-e
QLOUD_REDEPLOY_PREPARING        // Host becoming prepared and assigned/ready in wall-e
QLOUD_REDEPLOY_ADDING           // Host becoming part of The Qloud

QLOUD_REDEPLOY_BUFFER_BUSY            // Buffer host is in production segment
QLOUD_REDEPLOY_BUFFER_FREE            // Buffer host is doing nothing
QLOUD_REDEPLOY_BUFFER_RELEASE_PENDING // Buffer host wants to be free ond waiting for OK
QLOUD_REDEPLOY_BUFFER_RELEASING       // Buffer host waiting for services to disappear
```