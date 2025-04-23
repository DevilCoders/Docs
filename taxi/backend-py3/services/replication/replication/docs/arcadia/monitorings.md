## Монран
Запустите **monrun** на хостах сервиса **replication-tasks**.

Пример использования через **nuter**:
* **testing**: `nuter ssh taxi_replication-tasks_testing -p 2222 monrun -t replication`
* **production**: `nuter ssh taxi_replication-tasks_stable -p 2222 monrun -t replication`

Также нужно вступить в специальные чатики, куда будут прилетать алерты:
* **testing**: [{{ link_to_tg_testing_invite }}]({{ link_to_tg_testing_invite }})
* **production**: [{{ link_to_tg_production_invite }}]({{ link_to_tg_production_invite }})
