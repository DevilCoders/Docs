[async-profiler](https://github.com/jvm-profiling-tools/async-profiler) завёрнутый в ресурс MARKET_JAVA_ASYNC_PROFILER

Установка в nanny-сервис:
-------------------------
```
cd arc/market/mbo/scripts/nanny-utils
python3 inject_async_profiler.py --activate your-service and-another-one
```

Использование:
--------------
```
ssh {container} "async-profiler/profiler.sh -e wall -o flamegraph -d 5 jps" > result.html
```

Profile specific class/method:
```
ssh {container} "async-profiler/profiler.sh -e wall -o flamegraph -d 5 -I *.ClassName* jps" > result.html
```

Как обновить ресурс:
--------------------
1.
    ```
    ./build.sh
    ya upload --ttl=inf -T=MARKET_JAVA_ASYNC_PROFILER -d "Packaged async-profiler, checkout https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/scripts/java-async-profiler" temp/async-profiler.tar.gz
    ```
2. Зайти в Sandbox Task и зарелизить, чтобы у всех обновилось.
3. Надо обновить id ресурса в `inject_async_profiler.py`
