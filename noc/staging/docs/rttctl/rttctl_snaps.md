## rttctl snaps

list snapshots

### Options

```
  -a, --after string       time, after which snapshots should be created (YYYY-MM-DD HH:mm)
  -b, --before string      time, before which snapshots should be created (YYYY-MM-DD HH:mm)
  -h, --help               help for snaps
      --snap-name string   name of snapshot
```

### Options inherited from parent commands

```
      --dc string             DC filter, dc1,dc2,!dc3
  -d, --debug                 debug mode
      --dev                   connect to dev instance.
      --env string            Main staging instance or dev. (default "stage")
      --gitlab_token string   gitlab token
  -j, --json                  JSON output
  -n, --node stringToString   Node filter, --node="name=n1.*" (default [])
      --rttctl_host string    host (default "test.racktables.yandex-team.ru")
      --rttctl_token string   token for RT staging API
  -t, --timeout duration      Query timeout (default 1m0s)
```

### SEE ALSO

* [rttctl](rttctl.md)	 - Manage RT test env
* [rttctl snaps cvs](rttctl_snaps_cvs.md)	 - list cvs snapshots
* [rttctl snaps mysql](rttctl_snaps_mysql.md)	 - list mysql snapshots

