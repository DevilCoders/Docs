# ReConf-Juggler-RTC - Hierarchical Juggler aggregates builder for RTC

Over [7k aggregates](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3DRTC&view=tiles) are managed by RTC SRE team using this builder.

## Disclaimer

All artifacts built by code derived from here MUST be canonized and tested;
nobody will keep backward compatibility otherwise.

You've been warned.

## Description

This is a collection of primitives (checks, check sets, builders, panels and
so on) for [ReConf-Juggler](../../../reconf_juggler) used to build and maintain
Juggler aggregates for Runtime Cloud.  
Primitives are specific for RTC, but may be overrided and reused if necessary.

## Deploy

Besides [per-commit deploys](./HOWTO.md#how-to-deploy-aggregates-to-juggler)
there is sandbox scheduler to deliver changes caused by external sources
(wall-e projects, tags and so on): [21336](https://sandbox.yandex-team.ru/scheduler/21336/view)
used to build and automatically deploy changed aggregates using last released
builder.

## Tests and canonization

In order to verify all changes made in aggregates, all results are canonized.  
This means any change in resulting aggregates will cause test faulire. Diff
should be inspected and, if change apropriate, test should be
[canonized](./HOWTO.md/#how-to-canonize-tests-data). Tests may be canonized
independently (per builder) or all together, canonizing root builder (builders
arranged hierarchically)

## How to use

See [HOWTO.md](HOWTO.md)

For basic concepts see [ReConf-Juggler](../../../reconf_juggler) and
[ReConf](../../../reconf)

## See also

[Juggler docs](https://docs.yandex-team.ru/juggler/)

## Feedback

Feel free to [make a ticket](https://st.yandex-team.ru/createTicket?type=1&priority=2&tags=juggler&queue=HOSTMAN)
if you spotted a bug or have a feature request.
