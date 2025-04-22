## Intro
This is user guide for unit context feature of hostmanager unit objects.
For motivation and ... please see [UNIT-CONTEXT.md](UNIT-CONTEXT.md).

## Object
Each object consists of two sub-objects:
  * meta - object meta data (and **CONTEXT** definitions)
  * spec - object specification

And `meta.ctx` allows us to:
  * define variables gathered in a `map<string, string>`
  * interpolate variable values into object string attributes (`'{ver}'.format({'ver': '1.3b''})`)

How we do that?
## Context
We need to instruct hostman machinery how we derive our context from host information. We do that in semi-structured way:
```proto
message Context {
    message Match {
        string exp = 1; // Python like expression, yields boolean
        string val = 2; // String value to be used if expression evaluated to true
    }

    message Var {
        string name = 1;
        repeated Match match = 2;
    }

    repeated string include = 1;
    repeated Var vars = 2;
}
```
where:
  * `include` - a list of host info attributes we **explicitly** depend.
  * `vars` - a list of variable definitions which we form based on `include`'d attributes.

### Include
A list of host attribute names. All available attributes are defined in `ya_salt.proto::HostInclude`:
  * `hostname` - host name, e.g 'sas1-5166.search.yandex.net'
  * `num` - consistent number in [0,99] span, based on hostname
  * `walle_project` - walle project id e.g rtc-mtn
  * `walle_tags` - walle tags list
  * `net_switch` - network switch identifier, e.g  sas1-s582
  * `gencfg_groups` - list of currently present gencfg groups
  * `location` - geo location taken from wall-e, e.g 'msk'
  * `dc` - data center, e.g 'sas'


### Vars
We need some variables which we define (declare and assign values) based on host attributes. We do it by
matching _expressions_ one by one until first match. Let's look at the example:
```yaml
vars:
  - name: "version"
    match:
      - exp: "has_tag('rtc.stage-prestable')"
        val: '73936352'
      - exp: "geo('sas')"
        val: '71262152'
      - exp: "default()"
        val: '27239202'
```
**Expression** is Python expression evaluated within restricted environment.

Each variable checked against expression in provided order (from first to last):
  * default value (if non matched) - `''` (empty string)
  * if expression yield `True` (or anything that is `bool(exp) is True`) - `val` is assigned to `version`

### Example
Let's trace machinery logic on this `ctx` example:
```yaml
include:
    - walle_tags
    - geo
vars:
  - name: "version"
    match:
      - exp: "has_tag('rtc.stage-prestable')"
        val: '73936352'
      - exp: "geo('sas')"
        val: '71262152'
      - exp: "default()"
        val: '27239202'
``` 
We begin with en empty context map:
```
ctx = {}
```
After includes we add host attributes into it:
```python
ctx = {'walle_tags': ['rtc.stage-stable'], 'geo': 'sas'}
```
After variable matching done, we end up with this:
```python
ctx = {'walle_tags': [...], 'geo': 'sas', 'version': '71262152'}
```

Thus we can choose flags (and values), define package versions, etc. Now let's use them!

## Unit in a context
TL;DR: All string values in unit protobuf spec are `.format(**ctx)`'ed and then executed.

Namely we apply ctx to:
  * `meta.version`
  * `meta.annotations`
  * `spec.*` - except `map<>` attributes (not implemented yet)

### Debugging
For debugging purposes we use `ya-salt -f <file-with-definitions>.yaml`:
  * `-I` - path to YAML file with manually defined host includes (can use `-I production` on RTC hosts)
  * `-E` - only to preprocess and print unit file definitions (mimics `gcc -E`).

Let's look at examples.
### Render only non-production
```shell script
$ cat include.yaml 
hostname: sas1-5166.search.yandex.net
num: 87
walle_project: rtc-mtn
walle_tags: ['yasm_monitored', 'rtc.stage-prestable']
gencfg_groups: ['ALL_SEARCH']
location: sas
dc: sas
$ ya-salt apply -E -I include.yaml -f daemon.yaml
meta:
  ctx:
    include:
      - location
    vars:
      - match:
          - exp: default()
            val: 1.0b
        name: ver
  kind: PortoDaemon
  name: juggler-agent-rtc
  version: 1.0b-sas
spec:
  packages:
    - name: juggler-client-core
      version: 1.0b
    - name: yandex-rtc-juggler-config-sas
      version: 1.0-6238270
  properties:
    cmd:
      - /usr/bin/juggler-client
      - 1.0b
      - /var/run/juggler-client.pid
      - --lock-file
      - /var/run/juggler-client.pid
      - --config-dir
      - /etc/juggler/
    controllers:
      devices: 'false'
    cpuGuarantee: 0.5c
    cpuLimit: 3c
    group: monitor
    isolate: 'false'
    memoryGuarantee: 600Mb
    memoryLimit: 2Gb
    user: monitor
    virtMode: host
```
#### Render only on production host
```shell script
$ ya-salt apply -E -I production -f daemon.yaml
meta:
  ctx:
    include:
      - location
    vars:
      - match:
          - exp: default()
            val: 1.0b
        name: ver
  kind: PortoDaemon
  name: juggler-agent-rtc
  version: 1.0b-sas
spec:
  packages:
    - name: juggler-client-core
      version: 1.0b
    - name: yandex-rtc-juggler-config-sas
      version: 1.0-6238270
  properties:
    cmd:
      - /usr/bin/juggler-client
      - 1.0b
      - /var/run/juggler-client.pid
      - --lock-file
      - /var/run/juggler-client.pid
      - --config-dir
      - /etc/juggler/
    controllers:
      devices: 'false'
    cpuGuarantee: 0.5c
    cpuLimit: 3c
    group: monitor
    isolate: 'false'
    memoryGuarantee: 600Mb
    memoryLimit: 2Gb
    user: monitor
    virtMode: host
```
## Helper functions
To save some typing some helper function are available in expressions.

#### h(hostname)
  * Doc: `True` if current host name matches provided as argument.
  * Args: host name or a list of host names.
  * Hint: if host name is a string (i.e. single host check) you can provide short name, 
  `.search.yandex.net` will be assumed.
  * Example:
```python
h('sas1-5166') or h(['man1-5655.search.yandex.net', 'vla1-1384.search.yandex.net'])
```

#### geo(name)
  * Doc: `True` if current host in provided geo location.
  * Args: location identifier (string), one of: `sas`, `man`, `vla`, `msk`.
  * Example: `geo('msk') or geo('sas')`

#### prj(name)
  * Doc: `True` if current host in provided WALL-E project.
  * Args: project identifier (string), e.g `rtc-yabs-mtn`.
  * Example: `prj('rtc-mtn') or prj('yt-hahn-nodes')`

#### has_tag(tag)
  * Doc: `True` if current host's WALL-E project has specified tag.
  * Args: tag value (string), e.g `rtc.stage-prestable`.
  * Example: `has_tag('rtc.stage-prestable)`

#### has_group(group)
  * Doc: `True` if current host has provided GENCFG group.
  * Args: group identifier (string), e.g `ALL_SEARCH`.
  * Example: `has_group('SAS_NANNY_SERVICE')`

#### perc(v)
  * Doc: `True` if current host "num(ber)" is less or equal to `v`.
  * Args: integer
  * Example: `prj("rtc-mtn") and perc(30)`

#### prestable()
  * Doc: `True` if WALL-E project marked as `prestable` (i.e has tag `rtc.stage-prestable`).
  * Example: `prestable()`

#### production()
  * Doc: `True` if WALL-E project marked as `production` (i.e has tag `rtc.stage-production`).
  * Example: `production()`

#### switch(v)
  * Doc: `True` if current switch matches provided as argument.
  * Args: switch name or a list of switch names.
  * Example:
```python
switch('sas1-s582') or switch(['sas1-s582', 'vla2-7s35'])
```

#### default()
  * Doc: always returns `True`, can be used as catch-all match.
  * Example: `default()`
