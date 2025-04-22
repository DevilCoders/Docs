# Сигналы с http/tcp проверок/действий

PodAgent генерирует следующие `deee` сигналы для http/tcp проверок/действий:

```
success                    // Сколько раз проверка/действие завершилось успешно

error                      // Сколько раз проверка/действие завершилось с ошибкой 
                           // Например connection refused, не 2XX код ответа для http проверки
                           // В этом сенсоре не учитывается timeout
                           
timeout                    // Сколько раз проверка/действие отрабатывала больше timeout и была из-за этого прервана

wrong_answer               // Только для http
                           // Сколько раз ответ сервера был с 2XX кодом, но содержимое ответа не совпадало с ожидаемым
```

На каждую `http` проверку/действие генерируются все 4 сигнала, на каждую `tcp` проверку генерируются только 3 сигнала.

При этом, если проверка отсутствует в спецификации, то для нее не будет сгенерированы сигналы.

Если рассмотреть на примере, `workload` с `http readiness`, `tcp liveness`, `http stop` и `no destroy` будет генерировать `4 (for readiness http check) + 3 (for liveness tcp check) + 4 (for container http stop) + 0 (for no destroy)` сигналов

Из-за лимита на количество сигналов, который равен 2000, при очень большом количестве объектов в спеке часть пользовательских сигналов может не доходить до yasm.

[Обращаем внимание, что это не единственные сигналы, которые отдает pod_agent.](user-sensors.md#limit)

## Http {#http}

Для http проверок/действий сигналы имеют вид:

```
network_http_<workload_id>_<check/action type>_<signal_type>_deee
```

Примеры:

```
network_http_MyWorkload_readiness_error_deee
network_http_MyWorkload_readiness_success_deee
network_http_MyWorkload_readiness_timeout_deee
network_http_MyWorkload_readiness_wrong_answer_deee

network_http_MyWorkload_liveness_error_deee
network_http_MyWorkload_liveness_success_deee
network_http_MyWorkload_liveness_timeout_deee
network_http_MyWorkload_liveness_wrong_answer_deee

network_http_MyWorkload_stop_error_deee
network_http_MyWorkload_stop_success_deee
network_http_MyWorkload_stop_timeout_deee
network_http_MyWorkload_stop_wrong_answer_deee

network_http_MyWorkload_destroy_error_deee
network_http_MyWorkload_destroy_success_deee
network_http_MyWorkload_destroy_timeout_deee
network_http_MyWorkload_destroy_wrong_answer_deee
```

##  Tcp {#tcp}

Для tcp проверок сигналы имеют вид:

```
network_tcp_<workload_id>_<check/action type>_<signal_type>_deee
```

Примеры:

```
network_tcp_MyWorkload_readiness_error_deee
network_tcp_MyWorkload_readiness_success_deee
network_tcp_MyWorkload_readiness_timeout_deee

network_tcp_MyWorkload_liveness_error_deee
network_tcp_MyWorkload_liveness_success_deee
network_tcp_MyWorkload_liveness_timeout_deee
```
