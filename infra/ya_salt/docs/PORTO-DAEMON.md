## Porto daemon management

Hostmanager can manage daemons that should be launched within porto containers. By manage means:
  * daemon package set is installed/updated
  * daemon is started in porto container according to specification.

Motivation can be found in [HOSTMAN-39](https://st.yandex-team.ru/HOSTMAN-39).

## User interface
We tried to mimic some systemd/upstart routines and protocols.

### Installation
To start a daemon one must:
  * put YAML/JSON file into `/etc/hostman/porto-daemons.d/` with arbitrary name, e.g. `juggler-client.yaml`
  * add [orly rule](https://a.yandex-team.ru/arc/trunk/arcadia/infra/orly/rules)
    named `porto-daemon-{name}` and apply it: `orlyctl apply-rule -f <created_rule_file>`

#### File format
Supported extensions are:
  * `.yml` or `.yaml`
  * `.json`

File content **MUST**:
  * be a mapping
  * have `meta` mapping with `name` attribute, see `ObjectMeta` protobuf message
  * have `spec` mapping with content according to `PortoDaemon` protobuf message

See [ya\_salt.proto](../proto/ya_salt.proto) for reference.

Example:
```yaml
meta:
  kind: "PortoDaemon"
  version: "2.3.2001221352"
  name: "juggler-agent-rtc"
  delete_requested: False
spec:
  properties:
    virt_mode: "host"
    cmd:
      - "/usr/bin/juggler-client"
      - "--pid-file"
      - "/var/run/juggler-client.pid"
      - "--lock-file"
      - "/var/run/juggler-client.pid"
      - "--config-dir"
      - "/etc/juggler/"
    isolate: "false"
    user: "monitor"
    group: "monitor"
    controllers:
      devices: "false"
    memory_guarantee: "600Mb"
    memory_limit: "2Gb"
    cpu_guarantee: "0.5c"
    cpu_limit: "3c"
  packages:
    - name: "juggler-client-core"
      version: "2.3.2001221352"
    - name: "yandex-rtc-juggler-config"
      version: "1.0-6238270"
```
### Execution
On every execution iteration hostmanager scans this directory and reads all files. For each valid
daemon specification it executes routines to bring daemon up to date - i.e install/update/restart etc.

## Termination
If container needs to be shut down (to update or remove) hostmanager will:
  * send `SIGTERM`
  * wait 10 seconds for graceful shutdown
  * issue `.Destroy` RPC call to Porto which results in `SIGKILL` signal being sent


## Package notes
  * All `apt-get install` calls will have `HOSTMAN=1` env variable set.
  This allows (hopefully) performing less actions (ie. manual demon restarts) if managed by hostman. 
 
### Removal
Removing daemon means:
  * destroying porto container
  * purging all associated packages

This **IS** a dangerous destructive action, thus it cannot be performed implicitly (e.g by simply removing a file).
Thus we need *a protocol* for explicit removal. To remove daemon from host:
  * modify description file so that it has `meta.delete_requested: true` attribute
  * wait until all hosts have this daemon removed
  * remove the file

### Monitoring
For each managed daemon hostmanager push to YASM following signals:
  * `porto-daemon-{name}-ready_thhh` signal with values `1` and `0` if daemon is ready or not respectively
  * `porto-daemon-{name}-respawn_count_thhh` how many times portod respawned container since last check
  * `porto-daemon-{name}-restart_count_thhh` how many times hostman restarted daemon since last check
  * `porto-daemon-{name}-running_thhh` signal with values `1` and `0` if daemon is running or crashed

All these signals gathered together in [HOSTMAN-PORTODAEMONS](https://yasm.yandex-team.ru/template/panel/HOSTMAN-PORTODAEMONS)
panel.

Among yasm signals some raw events pushed to juggler:
  * `porto-daemon-{name}-ready` - OK when ready, CRIT otherwise

All juggler raw events are marked by `porto-daemon` tag.

### Manual testing
One can always test porto daemon specification locally via `ya-salt apply -f <porto-daemon-definition>.yaml`. This will:
  * read object from file
  * apply needed changes
  * report current status.

### Troubleshooting
Loaded specifications and daemons status are saved internally and may be
inspected using `ya-salt spec` command:
  * spec: `ya-salt spec -o json | jq .portoDaemons`
  * status: `ya-salt status -o json | jq .portoDaemons`

When daemon respawns it's worthwhile to look in it's stderr:  
`portoctl get <name> stderr`

Also `grep porto-daemon /var/log/ya-salt.log` quite useful when porto container
doesn't start.
