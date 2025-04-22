# Инструмент для запуска локального YQL с локальным YT

### Запуск:
Для запуска выполните команду ниже в этой директории

```bash
ya make -ttt --test-disable-timeout --test-stderr -F main.py -DUSE_UDF_FOR_LOCAL_YQL="$USE_UDF_FOR_LOCAL_YQL"
```

В результате запустится тест, который поднимет локальные YT и YQL и выведет в консоль информацию о портах и адресах запущенных сервисов.
Прекратить его работу можно при помощи `CTRL+C`

Полезно для ускорения запуска локальных тестов, использующих yt и yql: можно поднять yt и yql один раз и в тестах обращаться к ним

{% note warning "Attention" %}

Убедитесь, что последовательные запуски ваших тестов без сброса состояния YT будут корректны, поскольку YT сохраняет состояние кипариса

{% endnote %}

### Работа с UDF

{% note warning "Attention" %}

Перед запуском убедитесь, что поместили в переменную окружения `USE_UDF_FOR_LOCAL_YQL` нужные вам UDF

Например:
```bash
export USE_UDF_FOR_LOCAL_YQL="ydb/library/yql/udfs/common/set ydb/library/yql/udfs/common/string ydb/library/yql/udfs/common/topfreq ydb/library/yql/udfs/common/re2"
```

Какие UDF вам нужны вы можете найти в ya.make файле тестов, которые планируете запускать, в секциях PEERDIR или DEPENDENCES

{% endnote %}

В случае если вы не укажите нужные UDF, то YQL выдаст ошибку:
```
Failed to find UDF function: <Имя функции>
```
