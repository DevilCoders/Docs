## Janitor

### Release
* Find the last released version [here](https://sandbox.yandex-team.ru/resources?type=RTC_TOOL_JANITOR)
* Clone the task and start it
* When task finishes – release it

### Run
The task runs with [this](https://sandbox.yandex-team.ru/scheduler/17558/view) scheduler.

Local running:
build with
```ya make -A```

run with ```./bin/janitor --help```

### Scenario terminate
```./bin/janitor finish --id <scenario_id>```

### Tokens, config files and environment variables:
OAuth token with access to:
* Wall-E
* StarTrek
* Bot
* ABC
* Qloud

`export OAUTH=XXXX-XXXXXXXX`
`echo XXXX-XXXXXXXX > ~/.oauth`
`./bin/janitor --oauth XXXX-XXXXXXXX`

TVM ticket
with access to RTC instance resolver

`export TVM=XXXXXXXX`
`./bin/janitor --tvm XXXXXXXX`

## Monitoring
* [Juggler checks](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc-janitor-sandbox)
* [Juggler raw events](https://juggler.yandex-team.ru/raw_events/?query=host%3Drtc-janitor-sandbox)
* [Reconf](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/reconf/builders/projects/janitor/builder.py)
* [Reconf](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/reconf/checks/janitor.py)
