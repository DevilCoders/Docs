| Resource       | Rate for 1 hour                                 |
|----------------|-------------------------------------------------|
| **Intel Broadwell** |
| 5% vCPU        | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c5|string }}   |
| 20% vCPU       | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c20|string }}  |
| 50% vCPU       | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c50|string }}  |
| 100% vCPU      | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c100|string }} |
| RAM (for 1 GB) | {{ sku|RUB|mdb.cluster.pg.v1.ram|string }}      |
| **Intel Cascade Lake** |
| 5% vCPU        | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c5|string }}   |
| 20% vCPU       | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c20|string }}  |
| 50% vCPU       | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c50|string }}  |
| 100% vCPU      | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c100|string }} |
| RAM (for 1 GB) | {{ sku|RUB|mdb.cluster.pg.v2.ram|string }}      |
| **Intel Ice Lake** |
| 50% vCPU       | {{ sku|RUB|mdb.cluster.pg.v3.cpu.c50|string }}  |
| 100% vCPU      | {{ sku|RUB|mdb.cluster.pg.v3.cpu.c100|string }} |
| RAM (for 1 GB) | {{ sku|RUB|mdb.cluster.pg.v3.ram|string }}      |

{% if audience == "cvos" %}

| Resource       | Rate for 1 hour                                 | With CVoS for 1 year                                                                                                                        | With CVoS for 3 years |
|----------------|-------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| **Intel Broadwell** |
| 5% vCPU        | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c5|string }}   | −                                                                                                                                           | − |
| 20% vCPU       | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c20|string }}  | −                                                                                                                                           | − |
| 50% vCPU       | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c50|string }}  | −                                                                                                                                           | − |
| 100% vCPU      | {{ sku|RUB|mdb.cluster.pg.v1.cpu.c100|string }} | −                                                                                                                                           | − |
| RAM (for 1 GB) | {{ sku|RUB|mdb.cluster.pg.v1.ram|string }}      | −                                                                                                                                           | − |
| **Intel Cascade Lake** |
| 5% vCPU        | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c5|string }}   | −                                                                                                                                           | − |
| 20% vCPU       | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c20|string }}  | −                                                                                                                                           | − |
| 50% vCPU       | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c50|string }}  | −                                                                                                                                           | − |
| 100% vCPU      | {{ sku|RUB|mdb.cluster.pg.v2.cpu.c100|string }} | {{ sku|RUB|v1.commitment.y1.mdb.pg.cpu.c100.v2|string }} ({{ sku|RUB|v1.commitment.y1.mdb.pg.cpu.c100.v2|cud.y1|discount|percent|string }}) | {{ sku|RUB|v1.commitment.y3.mdb.pg.cpu.c100.v2|string }} ({{ sku|RUB|v1.commitment.y3.mdb.pg.cpu.c100.v2|cud.y3|discount|percent|string }}) |
| RAM (for 1 GB) | {{ sku|RUB|mdb.cluster.pg.v2.ram|string }}      | {{ sku|RUB|v1.commitment.y1.mdb.pg.ram.v2|string }} ({{ sku|RUB|v1.commitment.y1.mdb.pg.ram.v2|cud.y1|discount|percent|string }})           | {{ sku|RUB|v1.commitment.y3.mdb.pg.ram.v2|string }} ({{ sku|RUB|v1.commitment.y3.mdb.pg.ram.v2|cud.y3|discount|percent|string }}) |
| **Intel Ice Lake** |
| 50% vCPU       | {{ sku|RUB|mdb.cluster.pg.v3.cpu.c50|string }}  | —                                                                                                                                           | —              |
| 100% vCPU      | {{ sku|RUB|mdb.cluster.pg.v3.cpu.c100|string }} | {{ sku|RUB|v1.commitment.y1.mdb.pg.cpu.c100.v3|string }} (-28%)                                                                             | {{ sku|RUB|v1.commitment.y3.mdb.pg.cpu.c100.v3|string }} (-43%) |
| RAM (for 1 GB) | {{ sku|RUB|mdb.cluster.pg.v3.ram|string }}      | {{ sku|RUB|v1.commitment.y1.mdb.pg.ram.v3|string }} (-35%)                                                                                  | {{ sku|RUB|v1.commitment.y3.mdb.pg.ram.v3|string }} (-52%) |

{% endif %}

