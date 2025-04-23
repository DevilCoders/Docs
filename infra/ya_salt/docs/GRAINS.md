## Available grains
  * By default salt provides a lot of grains like `ps`, we restrict that.
  * We have a bunch of custom grains which one can use.

Allowed grains list:
  * **location** `str` - host geo location (typically one of: "sas", "man", "vla", "msk")
  * **walle_dc** `str` - host datacenter (typically one of: "sas", "man", "vla", "iva", "myt")
  * **walle_project** `str` - walle project name, e.g 'rtc-mtn'
  * **walle_tags** `list[str]` - a list of project tags
  * **walle_switch** `str` - switch field from walle (e.g. "sas2-8s87")
  * **walle_rack** `str` - rack field from walle (e.g. "08.01.21")
  * **gencfg** `list[str]` - a list of gencfg groups on host
