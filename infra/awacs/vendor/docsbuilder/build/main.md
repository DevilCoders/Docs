
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| config_tag | string |  |  |  ||
|| addrs | list of [Addr](#Addr) |  |  |  ||
|| admin_addrs | list of [Addr](#Addr) |  |  |  ||
|| maxconn | int32 |  | `5000` |  ||
|| workers | int32 |  |  |   
Допускает использование следующих функций: `get_workers`. ||
|| thread_mode | bool |  |  |  ||
|| buffer | int32 |  | `65536` |  ||
|| log | string |  |  |   
Допускает использование следующих функций: `get_str_var`, `get_log_path`. ||
|| events | map[string, string] |  |  |  ||
|| enable_reuse_port | bool |  | `True` |  ||
|| disable_reuse_port | bool |  |  |  ||
|| private_address | string |  | `127.0.0.10` |  ||
|| default_tcp_rst_on_error | bool |  |  |  ||
|| tcp_fastopen | int32 |  |  |  ||
|| tcp_congestion_control | string |  |  |  ||
|| tcp_listen_queue | int32 |  |  |  ||
|| reset_dns_cache_file | string |  | `./controls/reset_dns_cache_file` |  ||
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