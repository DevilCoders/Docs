| Ресурс                             | Цена за 1 час                                      | 
| --- | --- |
| **Intel Broadwell** |
| 5% vCPU (**burstable**, 2 ГБ RAM)  | {{ sku|KZT|mdb.cluster.redis.v1.cpu.c5|string }}   | 
| 20% vCPU (**burstable**, 4 ГБ RAM) | {{ sku|KZT|mdb.cluster.redis.v1.cpu.c20|string }}  | 
| 100% vCPU (**high-memory**)        | {{ sku|KZT|mdb.cluster.redis.v1.cpu.c100|string }} | 
| RAM (за 1 ГБ)                      | {{ sku|KZT|mdb.cluster.redis.v1.ram|string }}      | 
| **Intel Cascade Lake** |
| 5% vCPU                            | {{ sku|KZT|mdb.cluster.redis.v2.cpu.c5|string }}   | 
| 50% vCPU                           | {{ sku|KZT|mdb.cluster.redis.v2.cpu.c50|string }}  | 
| 100% vCPU                          | {{ sku|KZT|mdb.cluster.redis.v2.cpu.c100|string }} |
| RAM (за 1 ГБ)                      | {{ sku|KZT|mdb.cluster.redis.v2.ram|string }}      |
| **Intel Ice Lake** |
| 50% vCPU                           | {{ sku|KZT|mdb.cluster.redis.v3.cpu.c50|string }}  | 
| 100% vCPU                          | {{ sku|KZT|mdb.cluster.redis.v3.cpu.c100|string }} | 
| RAM (за 1 ГБ)                      | {{ sku|KZT|mdb.cluster.redis.v3.ram|string }}      | 

{% if audience == "cvos" %}

| Ресурс                             | Цена за 1 час                                      | Цена с CVoS на 1 год                                                                                                                              | Цена с CVoS на 3 года |
|------------------------------------|----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| **Intel Broadwell** |
| 5% vCPU (**burstable**, 2 ГБ RAM)  | {{ sku|KZT|mdb.cluster.redis.v1.cpu.c5|string }}   | —                                                                                                                                                 | — |
| 20% vCPU (**burstable**, 4 ГБ RAM) | {{ sku|KZT|mdb.cluster.redis.v1.cpu.c20|string }}  | —                                                                                                                                                 | — |
| 100% vCPU (**high-memory**)        | {{ sku|KZT|mdb.cluster.redis.v1.cpu.c100|string }} | —                                                                                                                                                 | — |
| RAM (за 1 ГБ)                      | {{ sku|KZT|mdb.cluster.redis.v1.ram|string }}      | —                                                                                                                                                 | — |
| **Intel Cascade Lake** |
| 5% vCPU                            | {{ sku|KZT|mdb.cluster.redis.v2.cpu.c5|string }}   | —                                                                                                                                                 | — |
| 50% vCPU                           | {{ sku|KZT|mdb.cluster.redis.v2.cpu.c50|string }}  | —                                                                                                                                                 | — |
| 100% vCPU                          | {{ sku|KZT|mdb.cluster.redis.v2.cpu.c100|string }} | {{ sku|KZT|v1.commitment.y1.mdb.redis.cpu.c100.v2|string }} ({{ sku|KZT|v1.commitment.y1.mdb.redis.cpu.c100.v2|cud.y1|discount|percent|string }}) | {{ sku|KZT|v1.commitment.y3.mdb.redis.cpu.c100.v2|string }} ({{ sku|KZT|v1.commitment.y3.mdb.redis.cpu.c100.v2|cud.y3|discount|percent|string }}) |
| RAM (за 1 ГБ)                      | {{ sku|KZT|mdb.cluster.redis.v2.ram|string }}      | {{ sku|KZT|v1.commitment.y1.mdb.redis.ram.v2|string }} ({{ sku|KZT|v1.commitment.y1.mdb.redis.ram.v2|cud.y1|discount|percent|string }})           | {{ sku|KZT|v1.commitment.y3.mdb.redis.ram.v2|string }} ({{ sku|KZT|v1.commitment.y3.mdb.redis.ram.v2|cud.y3|discount|percent|string }}) |
| **Intel Ice Lake** |
| 50% vCPU                           | {{ sku|KZT|mdb.cluster.redis.v3.cpu.c50|string }}  | —                                                                                                                                                 | — |
| 100% vCPU                          | {{ sku|KZT|mdb.cluster.redis.v3.cpu.c100|string }} | {{ sku|KZT|v1.commitment.y1.mdb.redis.cpu.c100.v3|string }} (-30%)                                                                                | {{ sku|KZT|v1.commitment.y3.mdb.redis.cpu.c100.v3|string }} (-46%) |
| RAM (за 1 ГБ)                      | {{ sku|KZT|mdb.cluster.redis.v3.ram|string }}      | {{ sku|KZT|v1.commitment.y1.mdb.redis.ram.v3|string }} (-36%)                                                                                     | {{ sku|KZT|v1.commitment.y3.mdb.redis.ram.v3|string }} (-50%) |

{% endif %}
