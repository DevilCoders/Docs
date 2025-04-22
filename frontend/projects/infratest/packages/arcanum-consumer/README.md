# arcanum-consumer

[![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/si.ci.arcanum-consumer)](https://oko.yandex-team.ru/pkg/@yandex-int/si.ci.arcanum-consumer)

## Установка

```console
npm i @yandex-int/si.ci.arcanum-consumer --registry=https://npm.yandex-team.ru
```

## Использование

```js
const { ArcanumConsumer } = require('@yandex-int/si.ci.arcanum-consumer');

const consumer = new ArcanumConsumer({
    hostname: '<hostname>',
    topics: ['logbroker/topic'],
    clientId: 'logbroker/consumer',
    token: 'token'
});

// Возможные события указаны в Event.type в пакете @yandex-int/si.ci.arcanum-proto
// @see https://a.yandex-team.ru/arc_vcs/frontend/projects/ci/packages/arcanum-proto/out/proto.d.ts?rev=7d869e95386adca72fea057761050740a862f1f9#L98
consumer.on('arcHeadsUpdated', console.log);
consumer.on('error', console.error);

await consumer.connect();
```

## Переменные окружения

#### `ARCANUM_MAX_READ_MESSAGE_COUNT`

Максимальное количество сообщений в результате чтения топика из Logbroker. По умолчанию — 20.

##### Рекомендация по подбору значения параметра

Для подбора значения посмотрите на [график _Messages written_][lb-written-messages] (количество записанных сообщений в единицу времени) в [`/arcanum/prod/events/all`][lb-arcanum-events].
Значение параметра должно быть равным или больше чем максимальное значения записанных сообщений, иначе у вас образуется очередь из непрочитанных сообщений ([график _Unread messages_][lb-messages-by-last-read]).

#### `ARCANUM_MAX_READ_MESSAGE_LENGTH`

Максимальный допустимый размер одного сообщения в результате чтения топика из Logbroker в мегабайтах. По умолчанию — 100.

##### Рекомендация по подбору значения параметра

Logbroker [ограничивает размер][lb-message-limit] одного сообщения (Logbroker message) 120 мегабайтами.
Консьюмер читает сообщения батчами (Logbroker batch), которые отправляются консьюмеру в gRPC-сообщении (gRPC message).
Сообщение gRPC по умолчанию ограничено 4 мегабайтами.
См. иллюстрацию ниже.

```
+-----------------------------+
| +-------------------------+ |
| | +---------------------+ | |
| | | Logbroker message 1 | | |
| | +---------------------+ | |
| | | Logbroker message 2 | | |
| | +---------------------+ | |
| | |         ...         | | |
| | +---------------------+ | |
| | | Logbroker message N | | |
| | +---------------------+ | |
| |     Logbroker batch     | |
| +-------------------------+ |
|        gRPC message         |
+-----------------------------+
```

Параметр `ARCANUM_MAX_READ_MESSAGE_LENGTH` задаёт ограничение на размер сообщение в gRPC.
Его значения должен быть не меньше `ARCANUM_MAX_READ_MESSAGE_COUNT × Размер одного сообщение Арканума`, формально `ARCANUM_MAX_READ_MESSAGE_COUNT × 120МБ`.
Обычно никто не пишет 120&nbsp;МБ, фактический размер записанных сообщений можно посмотреть [графике _Bytes written_][lb-written-bytes] в [`/arcanum/prod/events/all`][lb-arcanum-events].

:notebook: На пике Арканум пишет 54&nbsp;КБ, таким образом можно было бы ограничиваться `ARCANUM_MAX_READ_MESSAGE_COUNT × 0.055МБ`, но мы перестраховались и увеличили значения по умолчанию до 100&nbsp;МБ.


[lb-message-limit]: https://logbroker.yandex-team.ru/docs/concepts/quotas_and_limits#limits
[lb-arcanum-events]: https://logbroker.yandex-team.ru/lbkx/accounts/arcanum/prod/events/all?page=statistics&type=topic&tab=writeMetrics&metricsFrom=1651128901616&metricsTo=1651733701616
[lb-written-bytes]: https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqproxy_writeSession&graph=auto&Account=arcanum&OriginDC=cluster&host=cluster&sensor=BytesWrittenOriginal&TopicPath=arcanum%2Fprod%2Fevents%2Fall&Topic=%21total&Producer=%21total&b=365d&e=
[lb-written-messages]: https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqproxy_writeSession&graph=auto&Account=arcanum&OriginDC=cluster&host=cluster&sensor=MessagesWrittenOriginal&TopicPath=arcanum/prod/events/all&Topic=!total&Producer=!total&b=1d&e=
[lb-messages-by-last-read]:https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqtabletAggregatedCounters&graph=auto&Account=arcanum&OriginDC=%2A&host=%2A&sensor=TotalMessageLagByLastRead&ConsumerPath=fei%2Fprod%2Ftrendbox-ci-events-consumer&TopicPath=arcanum%2Fprod%2Fevents%2Fall&partition=-&user_counters=PersQueue&stack=true&b=1d&e=

