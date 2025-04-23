## CallMeBack

### Abstract
Service that allows to register notifications that needed to be called back at given point in time.

Detailed docs are located in [doc](./doc) subdirectory.

#### Core features:
* **<1s total system delay** in regular case. This is the time from creation of event to
notification delivery, when event planned to be called back ASAP.
* Delay values for abnormal cases is limited to **order of seconds** (can be configured).
Network distruption that leads to inaccessability of callback target is not included.
* Designed for, but not limited to, **thousands events per second**.
Tens of thousands RPS can be achieved via DB horizontal scaling, if needed.
* Designed for, but not limited to, store **tens of millions of events**.
As above, DB horisontal scaling could be used if more events need to be stored.

#### Core implementation technologies:
* HTTP API separated from background workers, all written in **asyncio Python3**
* **PostgreSQL** as persistent events storage
* Fine-grained control over latency-throughput tradeoff via **pipelining with buffering** on events processing
* Horizontal linear scaling via **microsharding** and **distributed leaderless pub/sub**
* Business-logic is built on composable **actor-like cooperative coroutines**, which make code a bit cleaner


