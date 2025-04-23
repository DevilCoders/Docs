В точности одно из следующих полей должно быть указано: `rr`, `weighted2`, `hashing`, `active`, `rendezvous_hashing`, `pwr2`, `leastconn`, `dynamic`.  
В точности одно из следующих полей должно быть указано: `backends`, `generated_proxy_backends`.
#|
|| Имя | Тип | Обязательность | Дефолт | Описание ||
|| attempts | int32 | * |  |   
Допускает использование следующих функций: `count_backends`, `count_backends_sd`. ||
|| active_skip_attempts | int32 |  |  |  ||
|| connection_attempts | int32 |  |  |   
Допускает использование следующих функций: `count_backends`, `count_backends_sd`. ||
|| rr | [Rr](#Rr) |  |  |  ||
|| active | [Active](#Active) |  |  |  ||
|| weighted2 | [Weighted2](#Weighted2) |  |  |  ||
|| hashing | [Hashing](#Hashing) |  |  |  ||
|| rendezvous_hashing | [RendezvousHashing](#RendezvousHashing) |  |  |  ||
|| pwr2 | [Pwr2](#Pwr2) |  |  |  ||
|| leastconn | [Leastconn](#Leastconn) |  |  |  ||
|| dynamic | [Balancer2Module.Dynamic](#Balancer2Module.Dynamic) |  |  |  ||
|| balancing_policy | [BalancingPolicy](#BalancingPolicy) |  |  |  ||
|| backends | list of [Balancer2Backend](#Balancer2Backend) |  |  |  ||
|| generated_proxy_backends | [GeneratedProxyBackends](#GeneratedProxyBackends) |  |  |  ||
|| on_error | another module |  |  |  ||
|| on_fast_error | another module |  |  |  ||
|| attempts_file | string |  |  |  ||
|| fast_attempts | int32 |  |  |   
Допускает использование следующих функций: `count_backends`, `count_backends_sd`. ||
|| fast_503 | bool |  |  |  ||
|| attempts_rate_limiter | [AttemptsRateLimiter](#AttemptsRateLimiter) |  |  |  ||
|| disable_attempts_rate_limiter | bool |  |  |  ||
|| retry_non_idempotent | bool |  | `True` |  ||
|| use_on_error_for_non_idempotent | bool |  |  |  ||
|| rewind_limit | int32 |  |  |  ||
|| on_status_code | map[string, message] |  |  |  ||
|| return_last_5xx | bool |  |  |  ||
|| status_code_blacklist | list of string |  |  |  ||
|| status_code_blacklist_exceptions | list of string |  |  |  ||
|| hedged_delay | string |  |  |  ||
|| delay_settings | [Balancer2Module.DelaySettings](#Balancer2Module.DelaySettings) |  |  |  ||
|| check_backends | [Balancer2Module.CheckBackends](#Balancer2Module.CheckBackends) |  |  |  ||
|#