## rttctl gettoken

open url for getting token

### Synopsis

Client will try open https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5a70922036fa453f9b881142f21c4df8
Client finding token in --rttctl_token param. RTTCTL_TOKEN env var or in file ~/.config/rttctl/token

```
rttctl gettoken [flags]
```

### Options

```
  -h, --help   help for gettoken
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

