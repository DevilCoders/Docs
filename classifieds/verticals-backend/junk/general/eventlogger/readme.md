# EventLogger

Принимает события в следующей модели: 
[schema-registry](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/event/model.proto)

Обогащает события с помощью сервисов [bonsai](../bonsai) и [gost](../gost).

Отправляет обогащенные события в [брокер](https://github.com/YandexClassifieds/etc-mono/tree/master/services/broker) 