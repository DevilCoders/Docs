# ReConf-Juggler - Juggler hierarchical aggregates building framework

## Goal

Produce highly customizable and maintanable Juggler aggregates

## Disclaimer

All artefacts built by this framework MUST be canonized and tested; nobody
will keep backward compatibility otherwise.

You've been warned.

## Key features

* Check is a tree node and may contain subchecks.
* No external DSL by design (Python everywhere).
* All entities defined as classes and therefore inheritable (checks, check
  opts, checks sets, command line tools etc. - all).
* Arbitrary business logic in any place.
* Test friendly and heavily covered by tests itself.
* Resulting builder is a statically built python program.
* Checks tree building tools out of the box.

## Main entities

ReConf-Juggler is based on [ReConf](../reconf):

* __Check__ derived from ReConf's `ConfNode`
* __CheckOptHandler__ derived from `OptHandler`
* __CheckSet__ derived from `ConfSet`
* __CheckOptFactory__ from `OptFactory`
* __AbstractJugglerResolver__ and it's derivatives from `AbstractResolver`

Entities introduced here:

* __Builder__ - hierarchical builder with command line interface

## Aggregates build and deploy

Testenv and [Sandbox](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/reconf/reconf_juggler/README.md)
may be used for continuous delivery, see how it's done in
[ReConf-Juggler-RTC](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/juggler/reconf/HOWTO.md#how-to-deploy-aggregates-to-juggler)

Build/deploy stages will be reported to startrek when ticket id mentioned in
commit message and _robot-sre-rtc-mon_ have write access to the ticket.

## Examples

See [code examples](examples)  
[ReConf-Juggler-RTC](../rtc/juggler/reconf)  

## See also

[Reconf-Juggler builders doc](./BUILDERS.md)  

[ReConf](../reconf)  
[Juggler](https://docs.yandex-team.ru/juggler/)  

## Feedback

Feel free to [make a ticket](https://st.yandex-team.ru/createTicket?type=1&priority=2&tags=reconf-juggler&queue=HOSTMAN)
if you spotted a bug or have a feature request.
