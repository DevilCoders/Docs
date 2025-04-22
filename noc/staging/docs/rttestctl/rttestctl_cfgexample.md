## rttestctl cfgexample

Generates config full exmaple

### Synopsis

Config example:

```yaml
projects:
  rt:
    name: rt
    default_project: nocdev/racktables
    env_prefix: RT_YANDEX
    default_branch: master
  invapi:
    name: invapi
    default_project: nocdev/invapi
    env_prefix: RT_INVAPI
    default_branch: master
  rtapi:
    name: rtapi
    default_project: nocdev/rtapi2rr
    env_prefix: RT_RTAPI
    default_branch: master
base_path: /rt-zpool/rt
share_path: /usr/share/rttestctl
work_dir: ./
reports_dir: test-report
results_dir: test-result
gitlab_token: ""
base_url: ""
db:
  db_dsn: ""
  racktables_pwd: ""
  racktables_ro_pwd: ""
  mysync_stream_from: sas-mysql.net.yandex.net
tvm:
  token: ""
  port: 18080
cvs:
  enable: false
  ssh_port: 10022
  http_port: 10080
  https_port: 10443
log_level: info
consul:
  addr: localhost:8500
  service_name: test.racktables.yandex-team.ru
  id: ""
  weight: 1
  encrypt: ""
  retry_join:
  - vla-rt-staging.vla.yp-c.yandex.net
port: 3888
ssh_port: 2222
dc: ""
health_timeout: 1m0s
images:
  test:
  - name: noc-gitlab.yandex-team.ru:5000/nocdev/rt-docker/rt-test-tox
    pull: false
    auth_conf: ""
  - name: noc-gitlab.yandex-team.ru:5000/moonug/rt-docker/rt-test-tox
    pull: false
    auth_conf: ""
  - name: rt-test-tox
    pull: false
    auth_conf: ""
  mysql:
  - name: noc-gitlab.yandex-team.ru:5000/nocdev/rt-docker/rt-mysql
    pull: false
    auth_conf: ""
  - name: mysql:5.7
    pull: false
    auth_conf: ""
  nginx:
  - name: noc-gitlab.yandex-team.ru:5000/nocdev/rt-docker/rt-nginx
    pull: false
    auth_conf: ""
  - name: noc-gitlab.yandex-team.ru:5000/moonug/rt-docker/rt-nginx
    pull: false
    auth_conf: ""
  - name: rt-nginx
    pull: false
    auth_conf: ""
  fpm:
  - name: noc-gitlab.yandex-team.ru:5000/nocdev/rt-docker/rt-fpm
    pull: false
    auth_conf: ""
  - name: noc-gitlab.yandex-team.ru:5000/moonug/rt-docker/rt-fpm
    pull: false
    auth_conf: ""
  - name: rt-fpm
    pull: false
    auth_conf: ""
  cvs:
  - name: noc-gitlab.yandex-team.ru:5000/nocdev/rt-docker/rt-cvs
    pull: false
    auth_conf: ""
  - name: noc-gitlab.yandex-team.ru:5000/cvs/cvs/rt-cvs
    pull: false
    auth_conf: ""
  - name: rt-cvs
    pull: false
    auth_conf: ""
  alexandria:
  - name: noc-gitlab.yandex-team.ru:5000/nocdev/rt-docker/rt-alexandria
    pull: false
    auth_conf: ""
  - name: rt-alexandria
    pull: false
    auth_conf: ""
  dns:
  - name: noc-gitlab.yandex-team.ru:5000/nocdev/rt-docker/rt-dns
    pull: false
    auth_conf: ""
registries: {}
snapshots_keep_hourly: 24
snapshots_keep_daily: 7
snapshots_keep_weekly: 4
snapshots_keep_monthly: 12
run_cmd:
  test: allure
  test_report: allure generate allure-results --clean
  fpm: php-fpm
  rtapi: supervisord -c /etc/supervisord.conf
  cvs: ""
  alexandria: ""

```

```
rttestctl cfgexample [flags]
```

### Options

```
  -h, --help   help for cfgexample
```

### Options inherited from parent commands

```
      --baseUrl string             base url (default "https://n1.test.racktables.yandex-team.ru")
  -b, --base_path string           Base path (default "/rt-zpool/rt")
  -c, --config string              path to config file (default "/etc/rttestctl/config.yml")
  -s, --config_secret string       path to config file with secret (default "/etc/rttestctl/config.secret.yml")
  -d, --debug                      debug mode
      --dsn string                 DSN for mysql (default "root:pwd@tcp(127.0.0.1:3306)/racktables")
      --racktables_pwd string      Password for mysql user racktables
      --racktables_ro_pwd string   Password for mysql user racktables_ro
      --reports_dir string         directory with allure reports (default "test-report")
      --rtctl_host string          host (default "n1.test.racktables.yandex-team.ru")
      --rttctl_token string        token for RT staging API
      --test_result_dir string     directory with allure results (default "test-result")
  -t, --token string               gitlab token
      --tvm_port uint16            tvmtool port (default 18080)
      --tvm_token string           tvmtool token
  -w, --work_dir string            Work directory (default "./")
```

### SEE ALSO

* [rttestctl](rttestctl.md)	 - Manage RT test env

