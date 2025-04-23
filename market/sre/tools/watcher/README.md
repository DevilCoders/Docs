### Watcher
Утилита призванная наблюдать за различиями между текущим состоянием бэкендов в haproxy и состоянием сервисов в service discovery.
На данный момент работает только с yp.sd. В случае **увеличения количества** подов или
**изменения состава** подов в группах(читай endpoint-сетах) будет вызвана команда рефреша haproxy.
Команды рефреша haproxy и проверки стопкрана вызываются exec'ом и захардкожены в HandBrakeCommand и HaproxyRefreshCMD константах.


#### Параметры запуска
~~~
Usage of watcher:
  -dry_run

  -force_run

  -get_stats

  -haproxy_refresh_delay duration
    	 (default 5s)
  -haproxy_timeout duration
    	 (default 1h0m0s)
  -log_file string
    	 (default "/var/log/yandex/market/watcher/watcher.log")
  -log_level string
    	 (default "INFO")
  -primer_json_file string
    	 (default "/var/lib/yandex/market/haproxy/endpoints/yp.json")
  -run_lock_file string
    	 (default "/var/run/watcher.pid")
  -stat_file string
    	 (default "/tmp/watcher_stats.json")
  -version

  -yt_path string
    	 (default "//home/market_sre/watcher/development/test")
  -yt_proxy string
    	 (default "locke.yt.yandex-team.ru")
  -yt_token_path string
    	 (default "/etc/datasources/yt_token.sh")
~~~

Параметры можно задавать в конфигурационном файле, заданном в DefaultConfigPath(/etc/yandex/market-watcher/watcher.yaml) или аргументами командной строки.

* **dry_run** - запустит полную цепочку проверок, но не будет рефрешить haproxy
* **force_run** - зарефрешит haproxy принудительно, но только если отжат emerjlock.
* **get_stats** - выведет статистику(Кешируется в /tmp) вот в таком виде:
~~~
{
  "LastLockAcquiredTimestamp": 1626697501,
  "LastSuccessFinishTimestamp": 1626697501,
  "LastSuccessRunDurationSec": 0,
  "LastErrorTimestamp": 1626204376,
  "Errors": 22,
  "TotalLockedRuns": 1464,
  "LastRefreshCallTimestamp": 1626447007,
  "HaproxyRefreshTry": 1,
  "HaproxyRefreshSuccess": 1
 }
~~~
* **haproxy_refresh_delay** - задержка между получением распределенного лока и непосредственным запуском refresh
* **haproxy_timeout** - максимальное время ожидание распределенного лока и выполнения haproxy refresh
* **log_file** - путь до файла с логами
* **log_level** - уровень логирования
* **primer_json_file** - путь до статус-файла, созданного праймером
* **run_lock_file** - pid-файл
* **stat_file** - файл со статистикой
* **version** - выведет версию утилиты
* **yt_path** - путь в yt до лок-файла, нужен для распределенного лока
* **yt_proxy** - url yt
* **yt_token_path** - путь до датасорса с токеном yt

#### Алгоритм работы
- Запускаемся крону раз в 5 минут
- Чекаем конфигурацию. Приоритет: флаги, ENV, файл с конфигом(если есть)
- Проверяем run lock, если лок уже взят другим процессом выходим.
- Проверяем emerjlock, если кем-то залочен, выходим.
- Занимаем run lock
- Считываем данные из файла, созданного праймером
- Дергаем данные из YP.SD по группам(endpoint-сетам) прописанным праймером
- Проверяем force_run ключ, если выставлен дергаем рефреш принудительно.
- Проверяем dry_run ключ, если выставлен, не рефрешим haproxy даже если появились новые поды.
- Сравниваем 2 сета. Только в случае если в одну или несколько групп были добавлены новые поды или изменились их персистентные хостнеймы будет произведен рефреш.
- Если выставлен и force_run и dry_run победит force_run
- Любой запуск рефрешь из вышеперечисленных произойдет только, если не занят распределенный лок в yt. Это позволяет запускать refresh поочередно на всех нодах кластера(mslb, fslb,rslb,sslb) балансеров. Ждать возможности взять лок будем время указанное в haproxy_timeout.
- После взятия распределенного лока ждем дополнительно haproxy_refresh_delay для стабилизации кластера после рефреша ноды haproxy.
- Пишем статистику
- отпускаем все локи
- Завершаем работу


#### Особенности установки
- Собираем и выкладываем релизной машиной:
    https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/yandex-market-watcher
- Во время установки, конфиг /etc/yandex/market-watcher/watcher.yaml генерится postinst скриптом из /etc/yandex/market-watcher/watcher.tmpl, прописывается путь yt_lock_path согласно ENV_TYPE(testing,stable...) и класстеру(mslb,fslb,sslb...)

#### Debug
- Логи пишутся в /var/log/yandex/market/watcher/wathcer.log
