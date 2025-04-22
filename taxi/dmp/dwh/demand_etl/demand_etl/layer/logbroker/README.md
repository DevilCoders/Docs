# Logbroker

Для каждой поставки данных через LB нужно создать и настроить topic, читателя 
и раздать права. Настройку проще всего осуществить с помощью консольной команды 
[logbroker](https://wiki.yandex-team.ru/logbroker/docs/config/#konsolnajautilitalogbroker)

Посмотреть список ресурсов в аккаунте: `logbroker -s logbroker schema list /taxi-dwh`

Ресурсы разделены по папкам:

* `dev` - ресурсы для разработки
* `test` - ресурсы для тестирования
* `prod` - "боевые" ресурсы

## Создание топика и читателя

Далее создаем топик 

```
logbroker -s logbroker schema create topic /taxi-dwh/dev/test-topic -p 2
```

Для топика можно создать количесво партиций в топике и период хранения данных в топике.

При необходимости создаем консьюмера - читателя:

```
logbroker -s logbroker schema create consumer /taxi-dwh/dev/test-consumer
```

## Раздача прав

Для записи создаем TVM приложение, для полученного id выдаем права на запись:

```bash
logbroker -s logbroker permissions grant \
    --path /taxi-dwh/dev/test-topic \
    --subject 2006157@tvm \
    --permissions WriteTopic
```

Для чтения создаем еще одно TVM приложенияе, для полученного id выдаем права на чтение:

```bash
logbroker -s logbroker permissions grant \
    --path /taxi-dwh/dev/test-topic \
    --subject 2006157@tvm \
    --permissions ReadTopic
```

Провязываем TVM приложение с читателем

```bash
logbroker -s logbroker permissions grant \
    --path /taxi-dwh/dev/test-consumer \
    --subject 2006157@tvm \
    --permissions ReadAsConsumer
```

Связываем читателя и топик

```bash
logbroker -s logbroker schema create read-rule \
    --topic /taxi-dwh/dev/test-topic  \
    --consumer /taxi-dwh/dev/test-consumer \
    --all-original
```


