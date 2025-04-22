=== Pipeline configuration ===

Header describes configuration structs for current implementation of
eventus pipeline.

In one side it grants that all required arguments were passed into pipeline's
components.

In another side it prepend possibility to implement user's own convertion
from final implementation of configuration to required for eventus
pipeline.

Here's an example of implementation by end-user of pipeline's configuration:

```(cpp)
    namespace eventus::pipeline::config {

    using SinkCfg = taxi_config::order_events_producer_pipelines::Sink;

    template <>
    Sink::Sink(const SinkCfg& ext_config)
        : Sink(ext_config.name) {}

    }  // namespace eventus::pipeline::config
```

This internal configurtion used inside of pipeline builder.
See EFFICIENCYDEV-10436

