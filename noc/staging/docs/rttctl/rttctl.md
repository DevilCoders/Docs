## rttctl

Manage RT test env

### Options

```
      --dc string             DC filter, dc1,dc2,!dc3
  -d, --debug                 debug mode
      --dev                   connect to dev instance.
      --env string            Main staging instance or dev. (default "stage")
      --gitlab_token string   gitlab token
  -h, --help                  help for rttctl
  -j, --json                  JSON output
  -n, --node stringToString   Node filter, --node="name=n1.*" (default [])
      --rttctl_host string    host (default "test.racktables.yandex-team.ru")
      --rttctl_token string   token for RT staging API
  -t, --timeout duration      Query timeout (default 1m0s)
```

### SEE ALSO

* [rttctl alexandria](rttctl_alexandria.md)	 - return alexandria endpoints
* [rttctl color](rttctl_color.md)	 - set background color
* [rttctl completion](rttctl_completion.md)	 - Generates completion scripts
* [rttctl doc](rttctl_doc.md)	 - Generate documentation
* [rttctl gettoken](rttctl_gettoken.md)	 - open url for getting token
* [rttctl info](rttctl_info.md)	 - print env info
* [rttctl logs](rttctl_logs.md)	 - show logs for container
* [rttctl mysql](rttctl_mysql.md)	 - return cmd with settings for mysql
* [rttctl nodes](rttctl_nodes.md)	 - list RT test env nodes
* [rttctl ps](rttctl_ps.md)	 - list RT test env
* [rttctl rm](rttctl_rm.md)	 - remove RT env and clean resources
* [rttctl rtapi](rttctl_rtapi.md)	 - return cmd with export env for rtapi
* [rttctl selfupdate](rttctl_selfupdate.md)	 - Update current rttctl binary from server
* [rttctl setrw](rttctl_setrw.md)	 - change RW/RO mode
* [rttctl snaps](rttctl_snaps.md)	 - list snapshots
* [rttctl spawn](rttctl_spawn.md)	 - Spawn new RT and some other project test env
* [rttctl ssh](rttctl_ssh.md)	 - return ssh cmd
* [rttctl test](rttctl_test.md)	 - run testcontainer for id
* [rttctl testurl](rttctl_testurl.md)	 - return env testreport url
* [rttctl url](rttctl_url.md)	 - return env main url
* [rttctl version](rttctl_version.md)	 - Print version

