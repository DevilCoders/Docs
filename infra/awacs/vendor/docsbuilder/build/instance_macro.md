В точности одно из следующих полей должно быть указано: `include_upstreams`, `sections`.
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| config_tag | string |  |  |  ||
|| version | string |  |  |  ||
|| log_dir | string |  | `/place/db/www/logs` |  ||
|| public_cert_dir | string |  | `/dev/shm/balancer` |  ||
|| private_cert_dir | string |  | `/dev/shm/balancer/priv` |  ||
|| ca_cert_dir | string |  | `./` |  ||
|| maxconn | int32 |  |  |  ||
|| workers | int32 |  |  |  ||
|| thread_mode | bool |  |  |  ||
|| buffer | int32 |  |  |  ||
|| enable_reuse_port | bool |  |  |  ||
|| disable_reuse_port | bool |  |  |  ||
|| sections | map[string, [IpdispatchSection](#IpdispatchSection)] |  |  |  ||
|| include_upstreams | [IncludeUpstreams](#IncludeUpstreams) |  |  |  ||
|| private_address | string |  |  |  ||
|| default_tcp_rst_on_error | bool |  |  |  ||
|| tcp_fastopen | int32 |  |  |  ||
|| tcp_congestion_control | string |  |  |  ||
|| tcp_listen_queue | int32 |  |  |  ||
|| dns_ttl | string |  |  |   
Допускает использование следующих функций: `get_random_timedelta`. ||
|| worker_start_delay | string |  |  |  ||
|| worker_start_duration | string |  |  |  ||
|| coro_stack_size | int32 |  |  |  ||
|| coro_stack_guard | bool |  |  |  ||
|| unistat | [MainModule.Unistat](#MainModule.Unistat) |  |  |  ||
|| cpu_limiter | [MainModule.CpuLimiter](#MainModule.CpuLimiter) |  |  |  ||
|| sd | [MainModule.ServiceDiscovery](#MainModule.ServiceDiscovery) |  |  |  ||
|| state_directory | string |  |  |  ||
|| dynamic_balancing_log | string |  |  |   
Допускает использование следующих функций: `get_str_var`, `get_log_path`. ||
|| pinger_required | bool |  |  |  ||
|| pinger_log | string |  |  |   
Допускает использование следующих функций: `get_str_var`, `get_log_path`. ||
|| config_check | [MainModule.ConfigCheck](#MainModule.ConfigCheck) |  |  |  ||
|| storage_gc_required | bool |  |  |  ||
|| enable_matcher_map_fix | bool |  |  |  ||
|| shutdown_accept_connections | bool |  |  |  ||
|| shutdown_close_using_bpf | bool |  |  |  ||
|#