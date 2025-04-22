# @yandex-int/node-metrics

Package with default node.js metrics and helpers for measure duration

Interface for registry looks like:
```typescript
interface RegistryInterface {
    updateHistogram(name: string, value: number): this;
    incrCounter(name: string, value: number): this;
    updateGauge(name: string, value: number): this;
}
```

You are able to use any realizations you wish.

You have to set your registry first (on the start of your app):
```typescript
import { setRegistry, RegistryInterface } from "./src/index"
const registry: RegistryInterface;

setRegistry(registry);
```


There are some examples below.

* **gc metrics**
```typescript
import { startGCMetricCollector } from "./src/index"

startGCMetricCollector("service_gc"); // metric will be service_gc_duration_dhhh 
```

* **eventloop metrics**
```typescript
import { startEventLoopLagMetricCollector } from "./src/index"

startEventLoopLagMetricCollector("service_eventloop_lag"); // metric will be service_eventloop_lag_dhhh 
```

* **simple measurement of duration**
```typescript
import { startMeasureDuration } from "./src/index"

const stop = startMeasureDuration("duration");
stop();
```

* **measurement of function's execution duration**
```typescript
import { measureDuration } from "./src/index"

const res = measureDuration(() => "nothing", "do_nothing");
console.log(res);
```

* **measurement of async function's execution duration**
```typescript
import { measureDuration } from "./src/index"

const promiseWithText = measureDuration(async () => {
    return new Promise(resolve => setTimeout(() => resolve("nothing"), 100))
}, "wait_nothing");

promiseWithText.then(res => console.log(res));
```

* **decorator for measurement of duration**
```typescript
import { duration } from "./src/index"

class JustAnOrdinaryClass {
  @duration("say_hello")
  simpleMethod(): void {
    console.log("Hello");
  }

  @duration("say_async_hello")
  async simpleAsyncMethod(): Promise<void> {
    await new Promise(resolve => setTimeout(resolve, 100));
    console.log("Hello")
  }

  @duration("there_is_no_way_to_say_hello")
  methodWithError(): void {
    throw new Error("Something went wrong");
  }
}
```

