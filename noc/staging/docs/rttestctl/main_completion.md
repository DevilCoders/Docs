## main completion

Generates bash completion scripts

### Synopsis

To load completion run

. <(rttestctl completion)

To configure your bash shell to load completions for each session add to your bashrc

# ~/.bashrc or ~/.profile
. <(rttestctl completion)


```
main completion [flags]
```

### Options

```
  -h, --help   help for completion
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

* [main](main.md)	 - Manage RT test env

###### Auto generated by spf13/cobra on 18-Nov-2021
