## rttestctl serve

Start API server

```
rttestctl serve [flags]
```

### Options

```
      --dc string         DC name
  -h, --help              help for serve
  -P, --port uint16       API server port (default 3888)
      --ssh_port uint16   SSH server port (default 2222)
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

