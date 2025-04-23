
### Performance
Stress test was run against cluster with this configuration:
* 1-core API x 10
* 1-core Worker x 14
* 4-core PogstreSQL x 3 (PGaaS `medium` cluster)
* Qloud L3 + L7 balancers, 1 core each

Total: 38 cores

Test profile consists of creation events with notification time equals to now() plus little delay (10, 30, 60 seconds).
`API` app processes creation requests, `Worker` app notifies special `Target` at given time.
`Target` logs incoming notifications expected delivery time and actual delivery time, allowing to measure actual delay
(not taking into account wallclock deviations between machines).

Measured quantities:
* Events creation RPS
* Events creation latency
* Components CPU load
* Notification delay

#### 5k RPS on events creation

This test profile represents system under normal load.

Avg CPU load:

| Component | CPU Load   |
| :-------: | :--------: |
| Api       |  70%       |
| Worker    |  60%       |
| DB leader |  40%       |
| DB replica|40% / 100% *|

\* current implementation of workers creates load spikes on DB replica.

Latency:

| Quantile | Latency |
|  ------: |  -----: |
|    50%   |  50 ms  |
|    80%   |  70 ms  |
|    90%   |  90 ms  |
|    95%   |  110 ms |
|    98%   |  160 ms |
|    99%   |  270 ms |

Notification delay (subject for optimization):

| Quantile | Delay  |
|  ------: | -----: |
|    50%   |  240 ms|
|    80%   |  1.2 s |
|    90%   |  4.1 s |
|    95%   |  6.3 s |
|    98%   |  8.1 s |
|    99%   |  8.7 s |


#### 7k RPS on events creation

This test profile represents system working under heavy load.

Avg CPU load:

| Component | CPU Load   |
| :-------: | :--------: |
| Api       |  90%       |
| Worker    |  80%       |
| DB leader |  50%       |
| DB replica|50% / 100% *|

Latency:

| Quantile | Latency |
|  ------: |  -----: |
|    50%   |  100 ms |
|    80%   |  160 ms |
|    90%   |  200 ms |
|    95%   |  250 ms |
|    98%   |  320 ms |
|    99%   |  420 ms |

Notification delay (subject for optimization):

| Quantile | Delay  |
|  ------: | -----: |
|    50%   |  1.2 s |
|    80%   |  7.1 s |
|    90%   |  8.8 s |
|    95%   |  9.8 s |
|    98%   |  10.5 s|
|    99%   |  11.0 s|
