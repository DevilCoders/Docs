# Команды и пробы

На данной странице описаны пробы, которые поддерживает workload, и примеры их применения.
Кратко: поведение проб аналогично поведению [kubernetes container probes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes).

По умолчанию, все команды запускаются в cwd - `/` box'а, но мы настоятельно рекомендуем указывать полный путь.

## Liveness проба {#liveness}

Проверяет, "жив" ли процесс workload. Если проверка завершается ошибкой, pod_agent убьет workload `kill -9` и перезапустит его.

Если Ваше приложение способно само завершаться/падать в нездоровых ситуациях, можете не указывать `Liveness`; pod_agent автоматически перезапускает завершившееся приложение.

`Liveness` позволяет бороться с "дедлоками": если какое-то приложение работает очень долго, то оно может перейти в нерабочее состояние, которое можно исправить только полным перезапуском приложения.

Во время остановки workload `Liveness` не запускается.

Поле `TLivenessCheck` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L639-647):

### Liveness Container {#liveness-container}

Рассмотрим следующую конфигурацию:

```yaml
workloads:
- id: liveness_test_workload
  box_ref: box
  start:
    command_line: /bin/bash -c 'touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600'
  liveness_check:
    container:
      command_line: cat /tmp/healthy
      time_limit:
        initial_delay_ms: 10000
        min_restart_period_ms: 5000
        max_restart_period_ms: 5000
```

В данном примере `Liveness` проверяет наличие файла `/tmp/healthy` каждые 5 секунд (этот период задается полями `min_restart_period_ms` и `max_restart_period_ms`).

При этом у пробы выставлено поле `initial_delay_ms`, которое говорит о том, что перед первой проверкой надо подождать 10 секунд. Ваше приложение должно успевать запускаться за указанный период, в противном случае оно будет постоянно убиваться, и никогда не будет полноценно запущено, так что очень рекомендуется давать хотя бы 5 секунд на запуск перед первой проверкой `Liveness` даже самым простым приложениям.

Когда workload запускается, выполняется следующая команда:

```bash
/bin/bash -c 'touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600'
```

Первые 30 секунд файл `/tmp/healthy` будет существовать, и команда из `Liveness` будет завершаться без ошибок. После 30 секунды файл будет удален и `cat /tmp/healthy` завершится с ошибкой, это приведет к перезапуску основой команды workload.

### Http Liveness {#http-liveness}

`Liveness` не обязательно должен быть командой, он также может быть http запросом.

```yaml
workloads:
- id: liveness_test_workload
  box_ref: box
  start:
    command_line: ./server
  liveness_check:
    http_get:
      port: 8080
      path: /healthz
      expected_answer: All ok
      time_limit:
        initial_delay_ms: 5000
        min_restart_period_ms: 3000
        max_restart_period_ms: 3000
```

В данной конфигурации указано, что `Liveness` надо запускать каждые 3 секунды, при этом надо подождать 5 секунд перед первой проверкой.

Каждые 3 секунды будет делаться http запрос к серверу, запущенному основной командой workload, и слушающему 8080 порт. Если по ручке `/healthz` вернется код успешного завершения и ответом сервера будет `All ok`, то проверка будет считаться успешно пройденной.

Иначе, если вернется код не из промежутка от 200 до 299 или ответ сервера будет не `All ok`, то workload будет перезапущен.

Рассмотрим следующий пример сервера на go:

```go
http.HandleFunc("/healthz", func(w http.ResponseWriter, r *http.Request) {
    duration := time.Now().Sub(started)
    if duration.Seconds() > 10 {
        w.WriteHeader(500)
        w.Write([]byte(fmt.Sprintf("error: %v", duration.Seconds())))
    } else {
        w.WriteHeader(200)
        w.Write([]byte("All ok"))
    }
})
```

Первые 10 секунд сервер считается "живым": ручка `/healthz` возвращает 200 и строчку `All ok`, но потом она начинает возвращать 500 код и сообщение об ошибке.

Таким образом этот сервер будет перезапускаться каждые 10 секунд.

Проверить вашу ручку можно при помощи `curl -i localhost:<port>/<path>`.

`-i` указать важно, ибо ваше приложение может вернуть `All ok`, но с 500-ым кодом в `headers`, что затруднит процесс дебага:

```bash
$ curl localhost:80/ping -i
HTTP/1.1 500 Internal Server Error
Content-Type: application/json; charset=utf-8
Content-Length: 42
Date: Thu, 09 Apr 2020 15:26:20 GMT
Server: Python/3.7 aiohttp/3.6.2

All ok
```

При обычном `curl` это выглядит так:

```bash
$ curl localhost:80/ping
All ok
```

### Tcp Liveness {#tcp-liveness}

Tcp проверка проверяет успешность вызова connect(3) на указанный порт.

{% note tip %}

Вызов происходит на ipv6 адрес, так что если вы слушаете только ipv4, то проверка будет неуспешной.

{% endnote %}

В коде это реализовано вот так:

```cpp
TSockAddrInet6 addr("::1", port);
TInet6StreamSocket connectSocket(socket(AF_INET6, SOCK_STREAM | SOCK_NONBLOCK, 0));
i32 connectResult = connectSocket.Connect(&addr);
```

Пример конфигурации:

```yaml
workloads:
- id: liveness_test_workload
  box_ref: box
  start:
    command_line: ./server
  liveness_check:
    tcp_check:
      port: 8080
      time_limit:
        initial_delay_ms: 5000
        min_restart_period_ms: 3000
        max_restart_period_ms: 3000
```

## Readiness проба {#readiness}

Проверяет, готов ли процесс workload обрабатывать запросы.

Если `Readiness` не указан, workload считается "готовым" всегда.

Ниже описано поведение, когда `Readiness` указан:

* перед первым запуском `Readiness` workload считается "неготовым";
* падение процесса workload сбрасывает "готовность" в `False`;
* перед остановкой workload'а "готовность" сбрасывается в `False`, проверка больше не запускается;
* если для workload выставлен `target_state=removed`, workload считается "готовым", когда он остановился

Pod считается готовым обрабатывать запросы, когда все его workload'ы с указанным `Readiness` "готовы".

"Готовность" отображается в флажке в статусе pod'a: `pod.ready`. Аналогичный флажок `workload.ready` есть в статусе workload'а.

Я.Деплой использует `pod.ready` для:

* deployment orchestration: новая ревизия replica_set выкладывается в рамках допустимой деградации
* service discovery: Я.Деплой создает/удаляет endpoint pod'а (во всех endpoint_set's, в фильтры которых попадает pod) в соответствии со значением `pod.ready`. [Подробнее про Service Discovery](../../service-discovery.md).

Поле `TReadinessCheck` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L627-635):

### Readiness Container {#readiness-container}

Рассмотрим следующую конфигурацию:

```yaml
workloads:
- id: readiness_test_workload
  box_ref: box
  start:
    command_line: /bin/bash -c 'sleep 30; touch /tmp/ready_flag; sleep 30; rm -rf /tmp/ready_flag; sleep 600'
  readiness_check:
    container:
      command_line: cat /tmp/ready_flag
      time_limit:
        min_restart_period_ms: 6000
        max_restart_period_ms: 6000
```

В данном примере `Readiness` проверяет наличие файла `/tmp/ready_flag` каждые 6 секунд.

Поскольку параметр `initial_delay_ms` не задан, он считается равен 5 секундам (дефолтное значение, может измениться в будущем, так что не стоит на него полагаться), так что первая попытка проверить готовность будет произведена через 5 секунд.

Когда workload запускается, выполняется следующая команда:

```bash
/bin/bash -c 'sleep 30; touch /tmp/ready_flag; sleep 30; rm -rf /tmp/ready_flag; sleep 600'
```

Первые 30 секунд файл `/tmp/ready_flag` не будет существовать, и команда `cat /tmp/ready_flag` будет завершаться с ошибкой, все это время workload будет продолжать работать, но будет посылаться сообщение о том, что он не готов к работе.

После 30 секунд файл будет создан и `Readiness` проверка завершиться без ошибок. В этот момент wokrload перейдет в состояние `ready`.

Еще через 30 секунд файл `/tmp/ready_flag` будет удален, `Readiness` проверка завершиться с ошибкой, и workload будет переведен в не готовое состояние, но продолжит свою работу.

### Http Readiness {#http-readiness}

Полностью аналогичен Http Liveness, за исключением метода обработки ошибки проверки.

Пример конфигурации:

```yaml
workloads:
- id: readiness_test_workload
  box_ref: box
  start:
    command_line: ./server
  readiness_check:
    http_get:
      port: 8080
      path: /ready_check
      expected_answer: Hello my dear @yanddmi!
      time_limit:
        initial_delay_ms: 5000
        min_restart_period_ms: 3000
        max_restart_period_ms: 3000
```

### Tcp Readiness {#tcp-readiness}

Полностью аналогичен Tcp Liveness, за исключением метода обработки ошибки проверки.

Пример конфигурации:

```yaml
workloads:
- id: readiness_test_workload
  box_ref: box
  start:
    command_line: ./server
  readiness_check:
    tcp_check:
      port: 8080
      time_limit:
        initial_delay_ms: 5000
        min_restart_period_ms: 3000
        max_restart_period_ms: 3000
```

## О правильном написании Liveness и Readiness пробы {#liveness-readiness}

{% note warning %}

Очень важно понять что `Liveness` и `Readiness` **независимы**.

{% endnote %}

Это означает, что даже если приложение ни разу не прошло `Readiness` пробу, `Liveness` будет запущен, и при его падении приложение будет убито.

### Мотивация независимой работы `Liveness` и `Readiness` {#liveness-readiness-motivation}

По факту эти две пробы проверяют разные вещи: первая проверяет, живо ли приложение, а вторая проверяет, можно ли лить на него трафик.

Нельзя делать `Liveness` проверку только тогда, когда приложение отвечает ОК в `Readiness`, ибо мы не сможем разделить такие ситуации:

1. Пропала сеть - приложение работает в штатном режиме, но не готово принимать запросы. `Readiness` красный, `Liveness` зеленый. Ничего делать не надо.
1. С сетью все в порядке, но произошел deadlock в http сервере. `Readiness` красный, `Liveness` красный. Надо убивать приложение.

Нельзя не обращать внимание на результат `Liveness` пробы до первого ответа ОК в `Readiness`, так как в момент начальной инициализации окружения `Readiness` у многих может падать. Мы не можем различить такие ситуации:

1. Приложение генерирует окружение в штатном режиме, просто дольше, чем на это рассчитывали.
1. Приложение повисло при генерации окружения и никогда не сможет пройти `Readiness` пробу. Надо запустить `Liveness` и прибить приложение.

То есть, если Ваше приложение первые 40 минут своей работы генерирует себе окружение, то `Liveness` должен говорить что все в порядке, а `Readiness` должен говорить что еще рано лить трафик.

Ваша `Liveness` проба должна различать состояния: генерация окружения/ошибка при генерации окружения/штатная работа/ошибка при работе.

### Мотивация считать OOM и timeout в `Liveness` и `Readiness` ошибкой {#oom-timeout}

В случае OOM и timeout мы считаем, что проба завершилась с ошибкой.

Почему нельзя считать, что OOM и timeout `Liveness` - это ок:

1. поведение `Liveness` начинает отличаться от `Readiness`, что может запутать.
1. timeout http/tcp - всегда плохой знак, в то время как timeout контейнера может значить что просто машина загружена. Тут, опять же, можно попытаться сказать, что надо вести себя по разному для контейнеров и для http/tcp, но это только всех запутает.

Поэтому мы решили, что любое падение пробы это ошибка.

### Пример правильной работы `Liveness` с timeout {#liveness-timeout}

Рассмотрим вот такой пример — у нас есть какой-то сервис, который работает с пользователями.

В вечер пятницы на него возросла нагрузка, он справляется с работой, правда немного замедлился, и у него почти никогда нет свободных thread'ов для обработки новых запросов в http сервере.

Так же у нас настроен `Http Liveness`, он пытается сделать запрос к серверу, но, из-за большой нагрузки и отсутствия свободных thread'ов, получает timeout, в итоге мы убиваем рабочий сервер, и деградируем ваш сервис еще больше.

Чтобы избегать подобных ситуаций, надо в http клиенте выделить отдельный thread, который обрабатывает исключительно `Liveness` ручку.

## Stop policy {#stop-policy}

По умолчанию Я.Деплой останавливает приложения следующим образом:

1. Ждет когда приложение отработает хотя бы 5 секунд.
1. Посылает **корневому процессу** приложения `SIGTERM`.
1. Если приложение не завершилось за `30` секунд, посылает ему `SIGKILL`.

`SIGKILL` не посылается сразу, ибо не все приложения можно моментально убить. Например, если приложение обрабатывает запросы, ему надо сообщить, что не надо принимать новые запросы, и дать возможность завершить старые.

Но иногда, чтобы корректно завершить приложение, нужно что-то более сложное, чем простая посылка `SIGTERM`, или просто хочется обрабатывать не сигнал о завершении, а `http` ручку `/shutdown`.

Я.Деплой предоставляет возможность использовать `Stop policy` для возможности задать сценарий корректного завершения вашего приложения.

Попытка завершить приложение происходит в одном из следующих случаях:

1. Вы обновили конфигурацию workload или любого box, volume, layer, static_resource от которых зависит workload, сразу после обновления всех зависимостей workload приложение будет перезапущено.
1. Вы выставили у workload `target_state` в `removed`, в данном случае приложение будет завершено, и будет ожидать, когда `target_state` обратно будет переведено в `active`.
1. Pod переезжает на другую node (хост). В этом случае stop тоже вызывается.

Обратим внимание, что обновления зависимостей workload **не начинается до его полной остановки**, поэтому если процесс завершения приложения занимает три дня, то все эти три дня ни один из ресурсов, от которых зависит workload, не будет обновлен.

Так же если приложение упадет при выполнении `Stop policy` (будет ненулевой код возврата), то оно **не будет перезапущено**.

Если процесс вашего приложения отсутствует на момент начала остановки, `Stop policy` **не будет вызван ни разу**.

Поле `TStopPolicy` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=7009699#L682-701):

### Stop Container {#stop-container}

Рассмотрим следующую конфигурацию:

```yaml
workloads:
- id: stop_test_workload
  box_ref: box
  start:
    command_line: ./server run
  stop_policy:
    container:
      command_line: ./stop_server.sh
      time_limit:
        min_restart_period_ms: 180000
        max_restart_period_ms: 180000
        max_execution_time_ms: 60000
    max_tries: 3
```

В данном примере `Stop` пытается остановить сервер пользовательским скриптом `./stop_server.sh`.

Если скрипт завершится с **нулевым** кодом возврата, а сервер в это время все еще не будет остановлен, то сервер будет убит принудительно, без последующих попыток перезапустить `Stop`.

Если же код возврата **не нулевой**, данный скрипт будет запускаться до тех пор, пока сервер не будет остановлен, или количество запусков не достигнет `max_tries = 3`. После 3 попытки сервер будет убит принудительно.

Между попытками остановить сервер будет сделан перерыв, равный 3 минутам (этот период задается полями `min_restart_period_ms` и `max_restart_period_ms`).

Также если одна из попыток занимает больше минуты (заданой параметром `max_execution_time_ms`), то скрипт `./stop_server.sh` будет убит (`SIGKILL`), и начнет ожидать периода перезапуска.

### Http Stop {#http-stop}

`Stop` не обязательно должен быть командой, он также может быть http запросом.

```yaml
workloads:
- id: stop_test_workload
  box_ref: box
  start:
    command_line: ./server run
  stop_policy:
    http_get:
      port: 8080
      path: /shutdown
      any: true
      time_limit:
        min_restart_period_ms: 180000
        max_restart_period_ms: 180000
        max_execution_time_ms: 60000
    max_tries: 3
```

В данном примере `Stop` пытается остановить сервер, посылая ему http запрос на порт 8080 по пути `/shutdown`.

Если http запрос завершится успешно (вернется код из промежутка от 200 до 299, при этом ответ сервера может быть любым из-за `any: true`, при желании вместо `any: true` можно указать `expected_answer`), то сервер будет убит принудительно, без последующих попыток вызвать `Stop`.

Иначе, данный запрос будет делаться до тех пор, пока не выполнится успешно, или количество запросов не достигнет `max_tries = 3`. После 3 попытки сервер будет убит принудительно.

Между попытками остановить сервер будет сделан перерыв, равный 3 минутам (этот период задается полями `min_restart_period_ms` и `max_restart_period_ms`).

Также если одна из попыток занимает больше минуты (заданой параметром `max_execution_time_ms`), то http запрос будет прерван по `timeout` и следующий будет задан только после периода перезапуска.

### Unix Signal Stop {#unix-signal-stop}

Поле `TUnixSignal` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=7355052#L720-741):

Рассмотрим следующую конфигурацию:

```yaml
workloads:
- id: stop_test_workload
  box_ref: box
  start:
    command_line: ./server run
  stop_policy:
    unix_signal:
      signal: SIGINT
      time_limit:
        min_restart_period_ms: 180000
        max_restart_period_ms: 180000
    max_tries: 3
```

В данном примере `Stop` пытается остановить сервер, посылая ему `SIGINT`. **Сигнал будет посылаться только корневому процессу.**

Сигнал будет посылаться до тех пор, пока сервер не умрет, или не будет достигнут предел по количеству попыток, который равен `max_tries = 3`.

Между попытками послать сигнал будет сделан перерыв, равный 3 минутам (этот период задается полями `min_restart_period_ms` и `max_restart_period_ms`).

После последней (третьей) попытки послать сигнал будут сделен перерыв, который соответствует ожиданию между третьей и четвертой попыткой (в данном случае `time_limit` задан просто, и это будет еще три дополнительные минуты). Затем сервер будет убит принудительно при помощи `SIGKILL`.

## Destroy policy {#destroy-policy}

Иногда при полном удалении приложения с пода надо сделать какие-то дополнительные действия. Например, отправить последние логи на какой-то другой сервер.

Я.Деплой предоставляет возможность использовать `Destroy policy` для возможности задать сценарий корректного удаления вашего приложения с пода.

`Destroy` будет вызван только при полном удалении вашего workload из конфигурации (включая сценарий переезда пода). При этом перед вызовом `Destroy` приложение будет остановлено при помощи `Stop`.

`Destroy` будет вызван в любом случае, не зависимо от того, смог ли `Stop` корректно завершить приложение.

Поле `TDestroyPolicy` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L517-528):

### Destroy Container {#destroy-container}

Рассмотрим следующую конфигурацию:

```yaml
workloads:
- id: destroy_test_workload
  box_ref: box
  start:
    command_line: ./server run
  destroy_policy:
    container:
      command_line: ./send_logs.sh
      time_limit:
        initial_delay_ms: 5000
        min_restart_period_ms: 180000
        max_restart_period_ms: 180000
        max_execution_time_ms: 60000
    max_tries: 3
```

В данном примере `Destroy` пытается отправить последние логи на внешний сервер командой `./send_logs.sh`.

Если скрипт завершится с **нулевым** кодом возврата, то `Destroy` будет считаться выполненным успешно, и последующих попыток его запустить не будет.

Если же код возврата **не нулевой**, данный скрипт будет запускаться до тех пор, пока не вернется нулевой код возврата, или количество запусков не достигнет `max_tries = 3`. После 3 запуска попытки выполнить `Destroy` прекратятся, приложение (workload) будет удалено с пода.

После остановки сервера (в данном случае сервер будет остановлен при помощи `SIGKILL`, поскольку не указан `Stop`) и перед первой попыткой запустить `Destroy` будет произведена задержка, равная 5 секундам (она задана параметром `initial_delay_ms`).

Между попытками послать логи будет сделан перерыв, равный 3 минутам (этот период задается полями `min_restart_period_ms` и `max_restart_period_ms`).

Также если одна из попыток занимает больше минуты (заданой параметром `max_execution_time_ms`), то скрипт `./send_logs.sh` будет убит (`SIGKILL`), и начнет ожидать периода перезапуска.

### Http Destroy {#http-destroy}

`Destroy` не обязательно должен быть командой, он также может быть http запросом.

```yaml
workloads:
# Main workload
- id: destroy_test_workload
  box_ref: box
  start:
    command_line: ./server run
  destroy_policy:
    http_get:
      port: 8080
      path: /force_push_logs
      any: true
      time_limit:
        min_restart_period_ms: 180000
        max_restart_period_ms: 180000
        max_execution_time_ms: 60000
    max_tries: 3

# Logs transmitter
- id: logs_transmitter_workload 
  box_ref: box
  start:
    command_line: ./logs_transmitter run --port 8080
```

В данном примере `Destroy` пытается отправить последние логи на внешний сервер, при помощи помощи другого приложения, поднятого в том же box, посылая ему http запрос на порт 8080 по пути `/force_push_logs`.

Если http запрос завершится успешно (вернется код из промежутка от 200 до 299, при этом ответ сервера может быть любым из-за `any: true`, при желании вместо `any: true` можно указать `expected_answer`), то `Destroy` будет считаться выполненным успешно, и последующих попыток его запустить не будет.

Иначе, данный запрос будет делаться до тех пор, пока не выполнится успешно, или количество запросов не достигнет `max_tries = 3`. После 3 запроса попытки выполнить `Destroy` прекратятся, приложение (workload) будет удалено с пода.

Между попытками послать запрос будет сделан перерыв, равный 3 минутам (этот период задается полями `min_restart_period_ms` и `max_restart_period_ms`).

Также если одна из попыток занимает больше минуты (заданой параметром `max_execution_time_ms`), то http запрос будет прерван по `timeout` и следующий будет задан только после периода перезапуска.

## Init commands {#init-commands}

Иногда перед запуском приложения надо подготовить среду для его работы.

Я.Деплой предоставляет возможность использовать `Init` команды для возможности задать набор действий, которые будут выполнены перед стартом приложения.

Эти команды будут выполнены перед первым запуском приложения, после каждого обновления конфигураций workload или любого box, volume, layer, static_resource, от которых зависит workload.

{% note info %}

Эти команды **не будут выполнены**, если вы выставили у workload `target_state` в `removed`, а потом обратно вернули его в `active`.

{% endnote %}

Также обращаем внимание, что все `child` `Init` команды после ее завершения будут убиты (более точно, все соседи по `freezer cgroup`). Поэтому их нельзя использовать для запуска `self daemonize` процессов. Если вам нужен какой-то демон в контейнере, создайте отдельный `workload` и используйте [start команду](workload.md#start).

Почти всегда подготовить среду для работы можно при помощи `Init` команд box, которому принадлежит workload. Поэтому плохим примером использования `Init` команд в workload является распаковка ресурсов в какую-то дополнительную папку, это лучше стараться делать при помощи `Init` [команд box](../box.md#init).

Но есть случаи, когда пересобирать box с каждым изменением workload не хочется, но с изменением workload нужно сделать что-то дополнительно со средой для его корректной работы.

Например в workload при помощи секретов поставляется rsa ключ для ssh, и его надо каждый раз при обновлении класть в `~/.ssh/id_rsa`.

В [proto схеме](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L461-464) init команды workload являются `repeated TUtilityContainer` полем `TWorkload`.

### Пример использования {#init-commands-sample}

Рассмотрим следующую конфигурацию:

```yaml
workloads:
- id: init_test_workload
  box_ref: box
  env:
  - name: RSA_KEY
    value:
      secret_env:
        id: MyRsaKey
        alias: MyKeys
  - name: CONFIG_SERVER_ADDRESS
    value:
      literal_env:
        value: proxy.my_server.yandex-team.ru
  start:
    command_line: ./server run
  init:
  - command_line: /bin/bash -c 'mkdir -p ~/.ssh; echo -n $RSA_KEY > ~/.ssh/id_rsa'
  - command_line: /bin/bash -c 'rm -rf ~/config; mkdir ~/config; scp -r $CONFIG_SERVER_ADDRESS:/config_path/* ~/config'
    time_limit:
      min_restart_period_ms: 180000
      max_restart_period_ms: 180000
      max_execution_time_ms: 60000
  - command_line: ./patch_config.sh
```

Предположим, что у нас в конфигурации есть секрет `MyKeys:MyRsaKey`, соответствующий нашему ключу для ssh.

Перед запуском основной команды **последовательно** будут выполнены все `Init` команды.

Первая из них выполнит следующую команду:

```bash
bin/bash -c 'mkdir -p ~/.ssh; echo -n $RSA_KEY > ~/.ssh/id_rsa'
```
Это положит наш ключ в папку `.ssh`.

Вторая же команда:

```bash
/bin/bash -c 'rm -rf ~/config; mkdir ~/config; scp -r $CONFIG_SERVER_ADDRESS:/config_path/* ~/config
```
Будет пытаться скачать файлы конфигурации.

Причем, если эта команда завершится с **ненулевым** кодом возврата, она будет запускаться до тех пор, пока не завершится корректно.

{% note warning %}

Это также означает, что если в wokrload есть init команда, которая никогда не может завершиться корректно, то основное приложение никогда не запустится.

{% endnote %}

Между попытками запустить эту команду будет сделан перерыв, равный 3 минутам (этот период задается полями `min_restart_period_ms` и `max_restart_period_ms`).

Также если одна из попыток занимает больше минуты (заданой параметром `max_execution_time_ms`), то эта команда будет убита (`SIGKILL`), и начнет ожидать периода перезапуска.

Как только эта команда завершится корректно, будет выполнена последняя `Init` команда `./patch_config.sh`, которая делает патч к конфигу.

## Основные элементы схемы {#scheme}

### TTimeLimit (Политика рестартов) {#ttimelimit}

Пока что редактирование доступно только через dctl. Тикет на UI: https://st.yandex-team.ru/DEPLOY-959

Поле `TTimeLimit` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L353-371):

Интервал между запусками рассчитывается по формуле

```C
min(maxRestartPeriodMs, minRestartPeriodMs + restartPeriodScaleMs * (restartPeriodBackoff ^ step))
```

`step` считается с 0 и равен `max(0, ConsecutiveFailuresCounter - 1)` для `workload stop` и `workload destroy` и `max(0, ConsecutiveSuccessesCounter - 1)` для всех остальных команд и проб: `workload readiness`, `workload liveness`, `workload init`

{% note warning %}

Политика рестартов применима только к init/liveness/readiness командам/пробам, а также к настройкам stop/destroy policy. Start процесс автоматически перезапускается (не чаще раза в 10 секунд) pod agent'ом и политика рестартов для него не применяется.

{% endnote %}

### TUtilityContainer {#tutilitycontainer}

Поле `TUtilityContainer` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L649-688):

Выполняет указанную в `command_line` команду (**делает exec**, так что для использования `|, >, etc` надо оборачивать команду в `bash -c '<command>'`).

Команда считается выполенной успешно, если код возврата равен нулю.

В случает `timeout` команду убивают при помощи `kill -9`.

### THttpGet {#thttpget}

Поле `THttpGet` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L589-608):

Делает http запросы к серверу по пути `path` и порту `port`.
Пока делает запросы только на `localhost`, в будущем это может быть изменено [https://st.yandex-team.ru/DEPLOY-944](https://st.yandex-team.ru/DEPLOY-944)

Ответ считается успешным, если код возврата находится в промежутке от 200 до 299 и выполнено одно из условий:

* поле `any` выставлено в `true`
* поле `any` выставлено в `false` и ответ сервера в точности равен `expected_answer`

### TTcpCheck {#ttcpcheck}

Поле `TTcpCheck` схематизировано следующим [proto message](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=5908379#L610-616):

Tcp проверка проверяет успешность вызова connect(3) на указанный порт.

{% note warning %}

Вызов происходит на ipv6 адрес, так что если вы слушаете только ipv4, то проверка будет неуспешной.

{% endnote %}

В коде это реализовано вот так:

```cpp
TSockAddrInet6 addr("::1", port);
TInet6StreamSocket connectSocket(socket(AF_INET6, SOCK_STREAM | SOCK_NONBLOCK, 0));
i32 connectResult = connectSocket.Connect(&addr);
```
