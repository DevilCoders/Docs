Для запуска бенчмарков нужно:

```sh
ya make
```

Запуск всех бенчмарков в файле:
```sh
jdk/bin/java -cp les-jmh.jar ru.yandex.market.logistics.les.jmh.AesCipherUtilBenchmark
```

Запуск определенного бенчмарка в файле:
```sh
jdk/bin/java -cp les-jmh.jar ru.yandex.market.logistics.les.jmh.AesCipherUtilBenchmark encryptString
```
