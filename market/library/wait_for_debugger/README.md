Функция ```WaitForDebugger()``` ждет подключения отладчика к текущему процессу в случае если на диске есть файл с именем ```/tmp/<process_name>_wait_for_debugger```

```<process_name>``` берется из ```/proc/self/comm```, обычно это первые 15 символов имени исполнимого файла (к примеру, для ```host_metric_logger``` это ```host_metric_log``` и файл будет называться ```/tmp/host_metric_log_wait_for_debugger```)

Пример использования:
```
touch /tmp/host_metric_log_wait_for_debugger
ya make -t market/report/runtime_cloud/host_metric_logger/bin/ut/ --test-disable-timeout
ya tool gdb -p $(pgrep host_metric_log)
```
Примеры случаев, когда данная функция может быть полезна:
- Отладка старта процесса в RTC.
- Отладка внешних процессов в юнит-тестах.
