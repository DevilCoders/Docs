# ReConf - Hierarchical configurations building framework

## Goal

Produce highly customizable and maintanable hierarchical configs out of
extensible and reusable objects.

## Disclaimer

All confs built using this framework MUST be canonized and tested; nobody will
keep backward compatibility with you code otherwise.

You've been warned.

## Key features

* Configurarion is a tree node and may contain subconfs
* Configuration and all it's attributes may be subclassed
* Configuration is serializable to JSON immediately after build
* ReConf is not a generator, but mutator for provided hierarchical structure
* Config builder is a python program build on top of this framework

## Main entities

* __ConfNode__

  Conf is a dict controlled by handlers. Each handler declare keys it
  responsible for. Any key-value pair written to conf processed by according
  handler. Default value is set when no initial value provided for key.

* __ConfSet__

  Used as subnodes container for another conf or as standalone thing to
  represent bunch (forest) of conf nodes.

  By default turns into cortesian product out of passed initial key-val pairs
  and pre-defined branches.

* __OptHandler__

  Contain default values for declared keys and control inserting values passed
  by conf object.

* __OptFactory__ (optional)

  Object which allow to override conf opt handlers creation using extra logic.

## How it works

### Main workflow

Conf and it's opts handlers should be subclassed from provided by ReConf base
classes, filled with default data and implement custom logic (if any).

Implemented conf class initialized with desired hierarchical structure and
as a result, produce confs tree (or confs forest), which then should be
`built()` to have conf opts.

### There are more workflows

* Build from hierarchical structure with predeclared conf nodes types.

* Build conf on the fly - when conf instantiated with defaults and then it's
  opts and subconfs modified by external code.

* When opt handlers provided by opts factory.

All may be mixed for most flexible approach.

## Examples

[Cortesian](examples/cortesian)

[ReConf-Juggler examples](../reconf_juggler/examples)  
[ReConf-Juggler-RTC](../rtc/juggler/reconf)

## Testing results

Best way to control conf build results, for now, are canonizing tests.  
There are some helpers in [infra.reconf.pytest](pytest) to do it more
effectively, see [examples](examples/pytest/test_caninization.py)

## Feedback

Feel free to [make a ticket](https://st.yandex-team.ru/createTicket?type=1&priority=2&tags=reconf&queue=HOSTMAN)
if you spotted a bug or have a feature request.
