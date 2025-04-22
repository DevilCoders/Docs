MaRS — Market Recommendation Service
====

Made using [Shiny HTTP server](https://wiki.yandex-team.ru/market/report/infra/shinyhttp/).

## Build

```
username@host:~/arcadia/market/mars$ ya make
```

## Run

### Внешние сервисы

Чтобы поднять сервис, нужно в конфиге указать пути до внешних сервисов.

Самый простой способ - оставить дефолтный конфиг. Но если хочется
потестировать на своих инстансах, то придётся их поднять.

#### market report
Самый простой способ поднять репорт - это собрать его и запустить для теста в режиме сервера. Так поднимется индекс из тестов.

Например:
```
username@host:~/arcadia$ cd market/report/
username@host:~/arcadia/market/report$ ya make --dist -E --force-build-depends --add-result=pb2.py
username@host:~/arcadia/market/report$ cd lite
username@host:~/arcadia/market/report$ ./test_wizards.py -s 26753
```

#### market dj
Чтобы поднять dj, нужно пойти в dj/services/market и следовать инструкции

#### bigb
TODO

#### carter
TODO

### Логгирование

Перед тем как запускаться, надо настроить логгирование в файле конфига для запуска: [bin/config/mars-local.cfg](bin/config/mars-local.cfg).

Если вы хотите протестировать доставку сообщений в logbroker или настроить приближенноую к проду среду, то следует поменять Target для логов на UnifiedAgent и, соответственно, его запустить.

#### Запуск unified agent

Есть конфиг для локального запуска unified_agent: [bin/config/unified-agent-local.cfg](bin/config/unified-agent-local.cfg)

Перед тем как запускать агента нужно предоставить данные для аутентификации. Самый простой способ - это запросить OAuth token вот [здесь](http://oauth.yandex-team.ru/authorize?response_type=token&client_id=11515c5e5e994dfe8196ccfd6eb42dd8) и добавить его в переменные окружения:

```bash
username@host:~/arcadia/market/mars$ export LOGBROKER_TOKEN=<ваш токен>
```

Также нужно обновить конфиг с которым запускается unified_agent и добавить для выхода в logbroker данные аутентификации. Например, вот так это будет выглядеть для тестового топика some-topic:
```
# logbroker: some-topic
- input:
    plugin: grpc
    config:
      uri: localhost:port
  channel:
    output:
      plugin: logbroker
      config:
        endpoint: logbroker.yandex.net
        port: 2135
        topic: market-dj/mars/testing/some-topic
        codec: raw
        oauth:
          secret:
            env: LOGBROKER_TOKEN
```

Теперь чтобы запустить самого агента надо сделать следующее:

```bash
username@host:~/arcadia/market/mars$ ya make -r deploy/unified_agent
username@host:~/arcadia/market/mars$ ./deploy/unified_agent/unified_agent -c bin/config/unified-agent-local.cfg
```

В документации можно посмотреть описание конфига для выходов unified_agent: [тут](https://docs.yandex-team.ru/unified_agent/configuration/outputs). Обычно в разработке может понадобиться прописать именно свой выход, тогда как входы и всё остальное оставить неизменным.

#### promo-triggers-log

Для корректной работы Logfeller, необходим валидный desc-файл, сгенерированный для [promo_triggers.proto](lib/morda_cart_widget/promo/promo_triggers/proto/promo_triggers.proto). При изменениях в протобуфе сгенерировать desc-файл можно с помощью команды:

```bash
`arc root`/contrib/tools/protoc/bin/protoc --descriptor_set_out `arc root`/logfeller/configs/parsers/market-mars-promo-triggers.desc --proto_path `arc root` --proto_path `arc root`/contrib/libs/protobuf/src --include_imports --include_source_info -I. `arc root`/market/mars/lib/morda_cart_widget/promo/promo_triggers/proto/promo_triggers.proto
```

Можно заново сгенерировать ресурсы Logfeller'а командой (каждый раз при изменениях в протобуфе это делать не нужно):
```bash
cd `arc root`/logfeller/configs/parsers && ./update_makefile.sh
```

Также необходимо произвести переканонизацию теста:

```bash
cd market/mars/lib/morda_cart_widget/promo/promo_triggers && ya make -t --canonize-tests --token [token]
```

Значение токена можно получить по [ссылке](https://sandbox.yandex-team.ru/oauth/).

Более подробно о настройке поставки логов в yt через Logfeller можно прочитать [тут](https://wiki.yandex-team.ru/logfeller/parser/formats/#protobuf) и [тут](https://wiki.yandex-team.ru/logfeller/connection/).

#### recommendation-proto-log

По настройке см. promo-triggers-log

Сгенерировать desc-файл можно с помощью команды:

```bash
`arc root`/contrib/tools/protoc/bin/protoc --descriptor_set_out `arc root`/logfeller/configs/parsers/market-mars-recommendation-proto-log.desc --proto_path `arc root` --proto_path `arc root`/contrib/libs/protobuf/src --include_imports --include_source_info -I. `arc root`/market/mars/lib/log/proto.recommendation_record.proto
```

### Запуск mars

```
username@host:~/arcadia/market/mars$ cd bin && ./mars-serv -c config/mars-local.cfg -p 8080
```

## Tests

```
username@host:~/arcadia/market/mars$ ya make --add-result pb2.py -tt
```

### Troubleshooting

#### `(No such file or directory) util/system/file.cpp:856: can't open "secrets/push-client-tvm-secret`

 Если необходимо активировать запись FeatureLog или TraceLog в топик логброкера, потребуется создать файл с секретом `bin/secrets/push-client-tvm-secret`. Значение секрета можно найти самостоятельно в одной из машин, на которых развернут MaRS в деплое (смотри его путь в [deploy/config/mars.cfg](deploy/config/mars.cfg)). Несмотря на то, что этот секрет знают очень многие, его не рекомендуется хранить в аркадии.

*Небольшой хак. В файл с секретом можно написать что-то бессмыссленное, но MaRS скорее всего запустится и будет работать, проблемы будут где-то внутри Shiny.*
