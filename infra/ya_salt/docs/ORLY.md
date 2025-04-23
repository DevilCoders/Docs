## Orly integration
Hostmanager uses [O'RLY](https://wiki.yandex-team.ru/runtime-cloud/orly/) to "orchestrate" following activities:
  * if lo state has changed - we use `salt-state-apply` rule
  if we are bootstrapping (i.e. running `base` environment in salt) - we use `salt-state-apply-initial`  
  * if yasm pillar has changed - we use `hostman-yasm-{prestable,production}`
  * if we decide to reboot for kernel rolling update - `hostman-kernel-{production,prestable}`

**Beware:** If walle project for this host has `rtc.stage-prestable` tag - we use `-prestable` rules.

## Operation attributes
To check if we can perform certain activity on host - we issue `StartOperation` request with following attributes:
  * `id` - hostname
  * `labels` - we fill in:
    * `geo=` - taken from walle `geo` host attribute
    * `ctype=` - either production or prestable depending on walle tags
    * `prj=` - walle project value, e.g `rtc-mtn`

Thus one can use label selector in O'RLY rule to tweak actions on hosts.