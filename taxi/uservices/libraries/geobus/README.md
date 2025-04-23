# Geobus protocol library
geobus protocol is a protocol for communicating between providers of drivers geo
positions and related information, such as raw and adjusted positions, etas of
tracked drivers,  and consumers of said information.  It is  a flatbuffers protocol
over redis pubsub. This library provides publishers and listeners for the
protocol.

## High-level and low-level API
Library provides 2 sets of APIs:

1. Low-level API provides serialization/deserialization of fb-messages into low-level structures.
   Low-level structures do not utilize strongly-typed mebers for storing latitude, longitude
   and other geographical members. Low-level API also doesn't provide classes for reading from/writing to redis pubsub.
   Headers for low-level API are in include/geobus folder.
2. High-level API uses classes from geometry and gpssignal libraries to represent driver positions. It also
   provides listeners and writers from/to redis pubsub.
   Headers for high-level API are in include/clients/geobus folder.

It is recommended to use High-level API.

## Channels

There are N channels (redis pubsub channels) at the moment, each with its own protocol
1. raw positions channel: Georeceiver pushes raw drivers positions to this channel. Low-level structures and methods for working with this
channel are in <geobus/positions.hpp>. High-level listener for this channel is ::clients::geobus::GeobusPositionsListener and
publisher is ::clients::geobus::GeobusPositionsPublisher
2. adjust-tracks channel: Adjuster (e.g. yaga) publishes short adjusted track for every raw driver position, approximately 15 last adjusted points.
Low-level API is in <geobus/adjust_tracks.hpp>. High-level listener is ::clients::geobus::GeobusAdjustTracksListener and publisheris ::clients::geobus::GeobusAdjustTracksPublisher
3. edge-positions channel: Adjuster (e.g. yaga) publishes multiple possible adjusted positions for every raw one. Low-level API is in
<geobus/edge_positions.hpp>. High-level listener is ::clients::geobus::EdgePositionsListener, publisher is ::clients::geobus::EdgePositionsPublisher.
4. etas channel. Driver-route-watcher publishes etas and positions of tracked drivers into this channel
5. multi-positions channel. Multi-position incapsulates several raw (unadjusted)
   positions from different sources (GPS, LBS, Navi etc) into one structure.

All channels transmit 'messages', each message contains multiple positions aggregated over some period of time (usually 100ms).

## Creating new channel
See this page https://wiki.yandex-team.ru/taxi/backend/graph/geobus-new-channel/

## High-level API
High-level API deals with proper and user-friendly representation of data. Structures of high-level API are always valid.
Attempt to create an object with invalid data will result in std::invalid_argument exception.

That poses a question: what if listener received a message with 100 positions and one position out of a hundred was incorrect ? We can
discard whole message, but it seems excesive. Instead, listener drops all invalid low-level positions and gives the user only the
ones that are valid.
And because publisher accepts only high-level API structures, it will never send
incorrect data to the geobus.

There are several ways to utilize listener. The recommended one is to use ::geobus::components::GeobusListeners.
This class takes care of statistics and settings and other things in the future.

```cpp
class MyClass : public ::components::LoggableComponentBase {
public:
  MyClass(const ::components::ComponentConfig& config,
           const ::components::ComponentContext& context);

  void ProcessPayload(std::vector<::clients::geobus::DriverEdgePosition>&& payload) {
    // do something
  };
};

MyClass::MyClass(const ::components::ComponentConfig& config,
                                 const ::components::ComponentContext& context)
    : ::components::LoggableComponentBase(config, context) {
    // Listener is stored inside GeobusListeners component. No need to store in MyClass
    FindComponent<::geobus::components::GeobusListeners>().CreateEdgePositionsSubscription(
      [this](const auto&, auto payload) {
        ProcessPayload(std::move(payload));
      }
      );
}
```

If you need somethign non-standard, you can create listener directly and pass your callback into constructor.

```cpp
class MyClass : public ::components::LoggableComponentBase {
public:
  MyClass(const ::components::ComponentConfig& config,
           const ::components::ComponentContext& context);

  void ProcessPayload(std::vector<::clients::geobus::DriverEdgePosition>&& payload) {
    // do something
  };

private:
  std::shared_ptr<::clients::geobus::EdgePositionsListener> listener;
};

MyClass::MyClass(const ::components::ComponentConfig& config,
                                 const ::components::ComponentContext& context)
    : ::components::LoggableComponentBase(config, context) {
  listener = std::make_shared<clients::geobus::EdgePositionsListener>(
      "my_redis_client_name", "my_redis_channel_name",
      [this](const auto&, auto payload) {
        ProcessPayload(std::move(payload));
      },
      context);
}
```

This way allows only one consumer. If you need more than one, then use ::clients::geobus::GeobusListenerChannel template class that provides
two ::utils::AsyncEventChannel channels - for bulk messages and for single positions.

## Low-level API
Low-level API is being slowly deprecated in favor of working with flatbuffers
classes directly. Please do not use this classes anymore.

## Testing
There are several sets of testing faculties. Some are designed to work with data, some - with clients.

Firstly, there are generatos, e.g. ::geobus::test::PositionsGenerator and 
::geobus::generators::RandomPositionsGenerator. Generators - as name suggests -
generate random and pseudorandom object. Generators that do not have word
'Random' in their name all work from given unsigned uint variable called salt.
Every invocation of method with same salt will provide same (by operator==)
result. Random generators - e.g. ::geobus::generators::RandomPositionsGenerator
return random elements/positions/payloads on every invocation.

Here is how one can use generators:
@snippet src/clients/positions_listener_test.cpp GeneratorExample

Secondly, there are some additional classes-plugins, that provide functionality
that is usefull in tests. They usually inherit from apropriate generators to
simplify coding.  For example, ::test::geobus::EdgePositionsTestPlugin provides
functor to sort ::clients::geobus::DriverEdgePosition structures and
::test::geobus::GpsSignalTestPlugin provides method TestGpsSignalsAreClose to compare two signals
with precision supported by geobus.
@snippet src/lowlevel/track_point_conversion_test.cpp TestGpsSignalsAreCloseSnippet

And finally, there is a ::test::geobus::GeobusListenerTester template class and
channel-specific testers derived from it  - for example
geobus::clients::EdgePositionsListenerTester. Those classes allows you to
emulate incomming geobus messages in your tests.  This way you
can test your code that uses any of geobus listeners.

All test files are in include/geobus/test folder.
@snippet src/clients/edge_positions_listener_test.cpp ListenerTesterSnippet

## Stress testing (tanking)

There is an embeded tank functionality, that can be used to stress test your
service. They work like this:
1. An object - tank - is created inside service in GeobusListeners component -
   hence 'embedded'.
2. This tank can be set up by various means
3. It starts calling user-supplied callback - the one that is used to receive
   actual geobus messages - at specified intervals.

At the moment, there are two ways to control tank:
1. With taxi-config, Suitable for firing at testing/unstable environment
2. With local yaml service config. Suitable for firing at load environment

To enable tank, there must be a section 'tank' in channel settings and it must
have parameter 'enable' set to true. If 'enable' is false, tank is not
created. Not 'created and disabled', not 'created but not firing' - not present.
At all.
```yaml
    geobus-listeners:
        # System will take settings from this section in GEOBUS_EMBEDED_TANK
        tank-section-name: my_service_name
        # Channel settings
        edge-positions-channel-settings:
            enable: true
            channel-name: channel:yaga:edge_positions
            # Tank settings
            tank:
                # If set to false, tank will not be CREATED
                enable: true
```

Tanks are supported for all channels except 'adjust_tracks'

### Taxi config
Taxi-config [GEOBUS_EMBEDED_TANK](https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/GEOBUS_EMBEDED_TANK?name=GEOBUS) is used to control firing. This is usefull when firing at testing/unstable environment.
   
To set it up, use the following config in GeobusListeners component:
```yaml
    geobus-listeners:
        # System will take settings from this section in GEOBUS_EMBEDED_TANK
        tank-section-name: my_service_name
        # Channel settings
        edge-positions-channel-settings:
            enable: true
            channel-name: channel:yaga:edge_positions
            # Tank settings
            tank:
                # If set to false, tank will not be CREATED
                enable: true
                # With this mode, tank is controlled by GEOBUS_EMBEDED_TANK
                mode: taxi-config

```
This will enable tank for channel edge_positions. It will NOT activate it.
To activate it, you must add/modify GEOBUS_EMBEDED_TANK config. Add there
the following section
```json
# must match tank-section-name from yaml config
"my_service_name" : {
  # settings for tank for channel:yaga:edge_positions
  "channel:yaga:edge_positions" : {
     # See documentation to GEOBUS_EMBEDED_TANK for in-detailed explanation
     # of parameters
     "payload_per_sec" : 10000
     "messages_per_sec" : 4
  }
}
```
Tanks that are not present in section are stopped. Same goes if whole section
is missing. So, if you need to stop tank, just remove/rename your service section or
section for specific channel from config.

### Yaml config
In this case, all settings are placed directly in service's yaml config file.
They are read on service start and to change them, you will have to change
config and restart service.
Here is how to setup firing:
```yaml
        geobus-listeners:
            # System will take settings from this section in GEOBUS_EMBEDED_TANK
            tank-section-name: my_service_name
            # Channel settings
            edge-positions-channel-settings:
                enable: true
                channel-name: channel:yaga:edge_positions
                # Tank settings
                tank:
                    # If set to false, tank will not be CREATED
                    enable: true
                    # With this mode, tank is controlled by this config itself
                    mode: service-config
                    # Message is fired every X milliseconds
                    firing-interval: 50
                    # And has size equal to Y elements(positons)
                    payload-size: 5
```

## Statistics and Grafana
All listeners and publishers have statistics. Use method `GetStatsForPeriod()` to obtain it and publish it via standard means.

We provide 'geobus' layout to use in infra-cfg-grafs yaml files. If you use
::geobus::clients::GeobusListeners class, then using is easy:
Example:
```yaml
- geobus:
    auto: true
    type: edge_positions_listener
    path: ${env2:glob}.*.yaga-metrolog
    title_suffix: ' | Listener stats'
```

If, for some reason, you still use listeners directly, you need to specify path
to the statistics explicitly
Example:
```yaml
layout:
- geobus:
    type: positions_listener
    path: ${env}.*.yaga.yaga-positions-reader.this-shard.1min.listener-stats
    repeat_var: shard_num
    title_suffix: ' | Shard $shard_num'
    collapsed: true
- geobus:
    type: edge_positions_publisher
    path: ${env}.*.yaga.yaga-positions-writer.this-shard.1min.publisher-stats.edge-positions-publisher
    repeat_var: shard_num
    title_suffix: ' | Shard $shard_num'
```

geobus layout options are:

1. auto: indicates that services uses GeobusListeners
2. type: type of a listener/publisher. Supported types are: positions_listener,
   positions_publisher, edge_positions_listener, edge_positions_publisher,
   adjust_tracks_publisher, adjust_tracks_listener.
3. path: this one is complicated. If auto is set to true, then this is simply
   path to service in graphite. Otherwise, this must be path to target listener
   statistics
4. repeat_var: optional field. Instructs grafana to repeat dashboards over
   specified variable.
5. title_suffix: optional title suffix, usefull if you use 'repeat_var'
