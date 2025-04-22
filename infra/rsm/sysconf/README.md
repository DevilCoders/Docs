# SYSconf for RTC

## Monitoring
* [Solomon] (https://solomon.yandex-team.ru/?project=juggler&cluster=checks&service=push&graph=auto&l.juggler_host=*&l.status=crit&l.juggler_service=sysconf&b=1w&e=)
* [Juggler] (https://juggler.yandex-team.ru/raw_events/?query=service%3Dsysconf&statuses=CRIT)
* [Yasm] https://yasm.yandex-team.ru/template/panel/hostctl-unit/kind=timer-job;unit=yandex-sysconf
* [Hostctl] http://hm-prestable.in.yandex.net/units/yandex-sysconf

## Develop plugins
* `cp -r internal/plugin/example internal/plugin/new_plugin`
* Update required methods: **Name()**, **Doc()**, **Enable()**, **Disable()**, **IsApplicable()**, **Check()**
* add import to main.go like this:
`_ "a.yandex-team.ru/infra/rsm/sysconf/internal/plugin/new_plugin"`
* `ya make -tt`
* Commit

### Notes
* Sysconf supporting --force flag, it developed for critical things. Use force arg in **Enable()** and **Disable()** methods
when you have critical block of code which have to apply on start OS. Because sysconf run with --force flag only on start system.
