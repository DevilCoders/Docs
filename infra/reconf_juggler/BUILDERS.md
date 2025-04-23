# ReConf-Juggler builders reference

## Builders types

TODO

## Builders hierarchy

TODO

## Builder directory structure

Minimal recommended structure:
```
├── __init__.py
├── bin
│   ├── tests
│   │   └── ya.make
│   └── ya.make
├── builder.py
├── tests
│   ├── canondata
│   │   └── test_builder.test_default
│   │       ├── input
│   │       └── output
│   ├── test_builder.py
│   └── ya.make
└── ya.make
```

* `bin` cli binary, to be able to build aggregates independently (highly useful
   for debugging).
* `bin/tests` ensure cli is buildable and executable.
* `builder.py` entry point for builder lib.
* `tests/test_builder.py` build aggregates and compare to canonized aggregates.
* `tests/canondata` storage for canonized data, all it's content created
   automatically during canonization and should be committed with builder
   sources.
* `tests/canondata/<test_mod>/<test_func_name>/input` canonized external
   (resolved) data, such as wall-e projects, resolved hosts and so on.
* `tests/canondata/<test_mod>/<test_func>/output` canonized resulting
   aggregates to compare with.

See [canonization note](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/reconf/#tests-and-canonization) for more info about canonized tests.

## Examples

See [builders examples](examples)  

## See also

[ReConf-Juggler-RTC builders](../rtc/juggler/reconf)  

## Feedback

Feel free to [make a ticket](https://st.yandex-team.ru/createTicket?type=1&priority=2&tags=reconf-juggler&queue=HOSTMAN)
if you spotted a bug or have a feature request.
