# Прочитать данные из прода

## Сборка
Есть особенности: https://st.yandex-team.ru/DEVTOOLSSUPPORT-11664
Для сборки нужно использовать такую команду:
```
ya make -DENABLE_GLOBAL_PROTO --build=release
```

## Как получить oauth токен
https://logbroker.yandex-team.ru/docs/concepts/security#oauth


## Создать консумера
Делается один раз для каждого консумера
```
# Создаем консьюмера, которым будем читать данные 
./logbroker -s logbroker schema create consumer market-indexer/dev/manual-common-consumer

# Разрешаем читать данным консумером для abc группы индексатора
./logbroker -s logbroker permissions grant --path market-indexer/dev/manual-common-consumer --subject svc_marketindexer@staff --permissions ReadAsConsumer
```

## Раздать права на чтение и сделать отдельное правило чтения
Делается 1 раз для каждой пары consumer-topic
```
# Даем права на чтение топика для abc группы индексатора и создаем правило чтение для нашего консумера
./logbroker -s logbroker permissions grant --path market-indexer/testing/blue/datacamp-offers --subject svc_marketindexer@staff --permissions ReadTopic
./logbroker -s logbroker schema create read-rule --topic market-indexer/testing/blue/datacamp-offers --consumer market-indexer/dev/manual-common-consumer --all-original

./logbroker -s logbroker permissions grant --path market-indexer/prod/blue/datacamp-offers --subject svc_marketindexer@staff --permissions ReadTopic
./logbroker -s logbroker schema create read-rule --topic market-indexer/prod/blue/datacamp-offers --consumer market-indexer/dev/manual-common-consumer --all-original

./logbroker -s logbroker permissions grant --path market-indexer/testing/blue/datacamp-offers-to-miner --subject svc_marketindexer@staff --permissions ReadTopic
./logbroker -s logbroker schema create read-rule --topic market-indexer/testing/blue/datacamp-offers-to-miner --consumer market-indexer/dev/manual-common-consumer --all-original

./logbroker -s logbroker permissions grant --path market-indexer/prod/blue/datacamp-offers-to-miner --subject svc_marketindexer@staff --permissions ReadTopic
./logbroker -s logbroker schema create read-rule --topic market-indexer/prod/blue/datacamp-offers-to-miner --consumer market-indexer/dev/manual-common-consumer --all-original
```

## Читать данные
Теперь мы можем из под пользователя группы индексатора читать данные __не боясь__ что то сломать в тестинге или проде

Если вы знаете формат данных, который находится в топике, то можно считать его и распарсить. Список известных форматов можно расширить [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/pqtool/src/main.cpp?rev=6900957#L68)
```
./pqtool --host sas.logbroker.yandex.net --lb-client-id market-indexer/dev/manual-common-consumer --only-original --mode read --read-count 1 --no-commit --output-format json --message-format Market.DataCamp.Offer --topic market-indexer/prod/blue/datacamp-offers --oauth-path ./oauth 2>/dev/null | jq .
``` 

Если вы хотите подготовить данные для теста, то рекомендуется формат ```json_base64```, в котором каждое сообщение будет записано на отдельной строчке в json формате с полей ```data```, где содержится сообщение, сериализованное в формат base64
```
./pqtool --host sas.logbroker.yandex.net --lb-client-id market-indexer/dev/manual-common-consumer --only-original --mode read --read-count 10 --no-commit --output-format json_list --message-format Market.DataCamp.Offer --topic market-indexer/prod/blue/datacamp-offers --oauth-path ./oauth 2>/dev/null | jq .

./pqtool --host vla.logbroker.yandex.net --lb-client-id market-indexer/dev/manual-common-consumer --only-original --mode read --read-count 2 --no-commit --output-format json_list --message-format Market.DataCamp.OffersBatch --topic market-indexer/prod/blue/datacamp-offers-to-miner --oauth-path ./oauth 2>/dev/null | jq .
```

## Писать данные

Например после того, как мы прочитали данные из продакшена
```
./pqtool --host vla.logbroker.yandex.net --lb-client-id market-indexer/dev/manual-common-consumer --only-original --mode read --read-count 2 --no-commit --output-format json_list --message-format Market.DataCamp.OffersBatch --topic market-indexer/prod/blue/datacamp-offers-to-miner --oauth-path ./oauth 2>/dev/null | jq . > /home/ymoskalenk0/src/arcadia/market/idx/datacamp/miner/tests/data/datacamp-offers-to-miner
```
Мы захотели запушить эти же данные в протоформате в топики в локальном логброкере, чтобы подебажить. Сделать это можно вызвать ```pqtool``` в режиме записи данных 

```
$ ./pqtool --host localhost --port 17836 --source-id test --input-file /home/ymoskalenk0/src/arcadia/market/idx/datacamp/miner/tests/data/datacamp-offers-to-miner --mode write --output-format json_list --message-format Market.DataCamp.OffersBatch --topic miner_input
```
