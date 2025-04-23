This library contains utilities for per-shard metric management.

`TResourceUsageContextBase` is the class you would usually want to use when extending metric set. It already contains some essential counters for CPU/memory/network. New metrics can be added by overriding the `Init(NMonitoring::IMetricFactory&)` method.
```C++
struct TMyShardContext: public TResourceUsageContextBase {
    void Init(IMetricFactory& f) {
        Something = f.Rate(new TLabels{{"metric", "something"}});
        SomethingElse = f.Counter(new TLabels{{"metric", "somethingElse"}});
    }
    
    IRate* Something;
    ICounter* SomethingElse;
};
```

After defining your own class for metrics you can use it to create a repository from the `TRepository` template:

```C++
struct TMyRepository: TRepository<TMyShardContext> {
};
```

That's it. Now metrics for an arbitrary shard can be created via `TMyRepository` by calling `std::shared_ptr<TMyShardContext> GetContext(TString project, TString shard)`.

Repository does not hold a reference to the context object, so context is destroyed when the last reference obtained via this method dies and corresponding metrics are not written to `IMetricConsumer` anymore.

Repository as a metric provider will also aggregate per-project and grand total counters.

#### TImmutableRegistry
`TImmutableMetricRegistry` (the word "immutable" here refers to the set of metrics, but not to their values) is a lightweight implementation of `IMetricSupplier` with some specific features:
- Values from two objects can be summed up. Note that there are no checks on whether or not labels/metric types match. So, both objects must contain the same set of metrics;
- Object can be cloned. Metric values of the clone object are reset to zero. This operation is pretty cheap since we allocate metrics on an arena and labels are shared between the objects;
