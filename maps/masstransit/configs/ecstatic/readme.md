## `default.switch`
Default ecstatic switch script to be used when multiple
datasets are deployed to a single service.

**Caution**: Service will be restarted in all environments except the `load`.

#### Usage:
Put a copy of this script into the
`/etc/template_generator/templates/etc/yandex/maps/ecstatic/<dataset>/` folder
for each dataset deployed to the service.


## `alive.check`
Default ecstatic check hook which checks whether the service responds to `/ping`.

#### Usage:
Put a copy of this script into the `/etc/yandex/maps/ecstatic/` folder.


## `preserve_data.conf`
Ecstatic config file which enables preserving latest dataset links in
`/var/lib/yandex/maps/ecstatic/preserved_data/`.

#### Usage:
Put a copy of this script into the `/etc/yandex/maps/ecstatic/conf.d/` folder.
