# Сигналы c контейнеров

PodAgent генерирует следующие `deee` сигналы для контейнеров box и workload:

```bash
killed_externally         // Количество завершений с кодом возврата < 0 (кроме OOM)
oom                       // Количество OOM
positive_return_code      // Количество завершений с кодом возврата > 0
zero_return_code          // Количество завершений с кодом возврата == 0
exited                    // Сумма killed_externally, oom, positive_return_code, zero_return_code

timeout                   // Количество timeout (работает для всего кроме start контейнера workload, у которого нет timeout)
                          // Обычно, после timeout контейнер убивается kill -9
system_failure            // Количество системных ошибок (например не удалось выполнить kill -9 контейнера)
```

На каждый box генерируется `7 * init_size` сигналов, на каждый workload `7 * (1 (for start container) + has_container_readiness + has_container_liveness + has_container_stop + has_container_destroy + init_size)` сигналов.

Если рассмотреть на примере, `workload` с `2 init` командами и `container stop` будет генерировать `7 (for start container) + 14 (for 2 init containers) 7 (for container stop)` сигналов

Из-за лимита на количество сигналов, который равен 2000, при очень большом количестве объектов в спеке часть пользовательских сигналов может не доходить до yasm.
[Обращаем внимание, что это не единственные сигналы, которые отдает pod_agent.](user-sensors.md#limit)

##  Box {#box}
Для box сигналы генерируются только для `init` контейнеров и имеют вид:

```bash
container_box_<box_id>_init_<init_number>_<signal_type>_deee
```

Нумерация для `init` контейнеров начинается с нуля.

Примеры:

```bash
container_box_TestBox_init_0_exited_deee
container_box_TestBox_init_0_killed_externally_deee
container_box_TestBox_init_0_oom_deee
container_box_TestBox_init_0_positive_return_code_deee
container_box_TestBox_init_0_system_failure_deee
container_box_TestBox_init_0_timeout_deee
container_box_TestBox_init_0_zero_return_code_deee
```

##  Workload {#workload}
Для workload сигналы генерируются для `start`, `readiness`, `liveness`, `stop`, `destroy`, `init` контейнеров и имеют вид:

```bash
container_workload_<workload_id>_<container_type>_<?init_number>_<signal_type>_deee
```

Нумерация для `init` контейнеров начинается с нуля.

Примеры:

```bash
container_workload_MyWorkload_destroy_exited_deee
container_workload_MyWorkload_destroy_killed_externally_deee
container_workload_MyWorkload_destroy_oom_deee
container_workload_MyWorkload_destroy_positive_return_code_deee
container_workload_MyWorkload_destroy_system_failure_deee
container_workload_MyWorkload_destroy_timeout_deee
container_workload_MyWorkload_destroy_zero_return_code_deee
container_workload_MyWorkload_init_0_exited_deee
container_workload_MyWorkload_init_0_killed_externally_deee
container_workload_MyWorkload_init_0_oom_deee
container_workload_MyWorkload_init_0_positive_return_code_deee
container_workload_MyWorkload_init_0_system_failure_deee
container_workload_MyWorkload_init_0_timeout_deee
container_workload_MyWorkload_init_0_zero_return_code_deee
container_workload_MyWorkload_init_1_exited_deee
container_workload_MyWorkload_init_1_killed_externally_deee
container_workload_MyWorkload_init_1_oom_deee
container_workload_MyWorkload_init_1_positive_return_code_deee
container_workload_MyWorkload_init_1_system_failure_deee
container_workload_MyWorkload_init_1_timeout_deee
container_workload_MyWorkload_init_1_zero_return_code_deee
container_workload_MyWorkload_liveness_exited_deee
container_workload_MyWorkload_liveness_killed_externally_deee
container_workload_MyWorkload_liveness_oom_deee
container_workload_MyWorkload_liveness_positive_return_code_deee
container_workload_MyWorkload_liveness_system_failure_deee
container_workload_MyWorkload_liveness_timeout_deee
container_workload_MyWorkload_liveness_zero_return_code_deee
container_workload_MyWorkload_readiness_exited_deee
container_workload_MyWorkload_readiness_killed_externally_deee
container_workload_MyWorkload_readiness_oom_deee
container_workload_MyWorkload_readiness_positive_return_code_deee
container_workload_MyWorkload_readiness_system_failure_deee
container_workload_MyWorkload_readiness_timeout_deee
container_workload_MyWorkload_readiness_zero_return_code_deee
container_workload_MyWorkload_start_exited_deee
container_workload_MyWorkload_start_killed_externally_deee
container_workload_MyWorkload_start_oom_deee
container_workload_MyWorkload_start_positive_return_code_deee
container_workload_MyWorkload_start_system_failure_deee
container_workload_MyWorkload_start_timeout_deee
container_workload_MyWorkload_start_zero_return_code_deee
container_workload_MyWorkload_stop_exited_deee
container_workload_MyWorkload_stop_killed_externally_deee
container_workload_MyWorkload_stop_oom_deee
container_workload_MyWorkload_stop_positive_return_code_deee
container_workload_MyWorkload_stop_system_failure_deee
container_workload_MyWorkload_stop_timeout_deee
container_workload_MyWorkload_stop_zero_return_code_deee
```
