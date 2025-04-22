## rttctl snaps cvs

list cvs snapshots

```
rttctl snaps cvs [flags]
```

### Options

```
  -h, --help   help for cvs
```

### Options inherited from parent commands

```
  -a, --after string          time, after which snapshots should be created (YYYY-MM-DD HH:mm)
  -b, --before string         time, before which snapshots should be created (YYYY-MM-DD HH:mm)
      --dc string             DC filter, dc1,dc2,!dc3
  -d, --debug                 debug mode
      --dev                   connect to dev instance.
      --env string            Main staging instance or dev. (default "stage")
      --gitlab_token string   gitlab token
  -j, --json                  JSON output
  -n, --node stringToString   Node filter, --node="name=n1.*" (default [])
      --rttctl_host string    host (default "test.racktables.yandex-team.ru")
      --rttctl_token string   token for RT staging API
      --snap-name string      name of snapshot
  -t, --timeout duration      Query timeout (default 1m0s)
```

### SEE ALSO

* [rttctl snaps](rttctl_snaps.md)	 - list snapshots

