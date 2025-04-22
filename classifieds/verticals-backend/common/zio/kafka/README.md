
### Добавляем кафка-консюмер в свой проект

В `application.conf` кладем конфиг следующего вида (который вы читаете как `ConsumerConfig`)

```hocon
consumer {
  bootstrap-servers = ${?KAFKA_BOOTSTRAP_SERVERS}
  topic = ${?KAFKA_TOPIC}
  group-id = ${?KAFKA_GROUP_ID}
  offset-reset-strategy = "EARLIEST"
  read-timeout = 10s
}
```

В классе вашего сервиса делаете подписку на топик следующим образом 

```
class Service(config: ConsumerConfig, env: Env) {

    private val (keyDeserializer, valueDeserializer) =
      (new StringDeserializer, new ProtobufDeserializer[YourProtobufMessage])

    private val kafkaReader =
      KafkaReader(config, keyDeserializer, valueDeserializer)

    override def consumeWith(eff: YourProtobufMessage => Task[Unit]): Task[Unit] = {
      kafkaReader.flatMap(_.subscribe(eff).useForever).provide(env)
    }
  }

```

