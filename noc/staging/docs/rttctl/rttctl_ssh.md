## rttctl ssh

return ssh cmd

```
rttctl ssh <envid> [fpm|api|mysql|nginx] [flags]
```

### Examples

```

Get shell at main rt container:
	`rttctl ssh <envid>`
Get shell at rtapi container
	`rttctl ssh <envid> api`
```

### Options

```
  -h, --help   help for ssh
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

