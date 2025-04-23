# Juggler aggregates dumpind tool

## Keep in mind

* Filter formed from `--namespace`, `--object-names`, `--service-names` and
`--tags` opts is used to retrieve initial aggregates set, which then dumped
recursively (if `--recursive` opt enabled).

* When no aggregates match filter API return empty aggregates set.

## FAQ

### How to build

Just run `ya make bin` in this directory.

If you unfamiliar with arcadia build ecosystem, read about
[ya tool](https://wiki.yandex-team.ru/yatool/) first.

### How to dump arbitrary aggregate as json

`jdump --recursive=1 --object-names rtc --service-names ssh`

where `object-name` is a `host` in Juggler notation.

### How to dump arbitrary aggregate as structure chart

Same as above, but add `--ofmt html` opt.
