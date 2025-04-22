# Checks collections

## Categories

Right now checks grouped by category:
 - **cloud** - top level checks, required for cloud work: `porto`, `iss`, etc.
 - **hardware** - all hardware checks (`raid`, `cpu`, `mem`, ...)
 - **informal** - diagnostic checks
 - **infrastructure** - low level infra checks (`cron`, `bind` and so on)
 - **jobs** - check that various sandbox schedulers works as expected
 - **monitoring** (yasmagent)
 - **network** - things related to network (IPs, MTU, fastbone, ...)
 - **portodaemons** - portodaemons, see  infra/ya\_salt/docs/PORTO-DAEMON.md
 - **unispace** - file system space checks
 - **unreachable** - `UNREACHABLE` and `META` checks

Abstract class for each category defined in according module.

This decomposition was inherited from earlier generator and will be revised in
the future.

## Classes

Minimal (and almost always sufficient) check class looks like this:
```
class raid(AbstractHardwareCheck):
    """Short, but sensible description of a class"""
    doc_url = 'https://example.org/path/to/doc.txt'
```

Major things here:
 - Name of the class turned to lowercase will be used for service name.
 - Parent of the class defines host dependencides; for example all checks
   depends on checks derived from `AbstractUnreachCheck` class.
 - ValidationError will be raised if docstring or `doc_url` absent.

Check should have `maintainers` attribute (tuple of strings) with staff
groups/logins if not maintained by RTC SRE team.

These (and many other) opts may be altered, see `Check` class in
[infra.reconf.juggler](../../../../reconf_juggler/__init__.py) and
[infra.rtc.juggler.reconf.checks](./__init__.py)
