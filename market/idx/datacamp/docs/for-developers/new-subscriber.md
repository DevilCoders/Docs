## Получение апдейтов по событийной модели

Подписка работает в два этапа, задействуя [controller-ы и dispatcher](../components/scheme#obshaya-shema). При попадании апдейта в контроллеры, они в транзакции пишут в стейт на динамических таблицах YT, а так же сообщение в [специальном формате](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/subscription/subscription.proto?rev=r9136171#L20) об измененных полях диспатчеру. При этом есть возможность помимо маски измененных полей передавать дополнительную информацию (например [список новых картинок](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/subscription/subscription.proto?rev=r9136171#L14)) для последующего использования в момент определения, что нужно/не нужно слать подписчику.

### Пошаговая инструкция для добавления нового подписчика { #how-to }

Давайте разберем пример добавления нового подписчика для нового татарского маркета.
#### Шаг 1
Расширяем [Market::ESubscriber](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/extension.proto?blame=true&rev=r9405994#L106) новым значением, в качестве идентификатор можно взять предыдущий + 1:
```
+++ market/idx/datacamp/proto/common/extension.proto

    CVDUP_IMAGES_SUBSCRIBER = 34;
    MINER_FULL_SUBSCRIBER = 35;
+   TATAR_MARKET_SUBSCRIBER = 36;
};
```
#### Шаг 2
В том же файле расширяем [FieldOptions](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/extension.proto?blame=true&rev=r9405994#L149), аналогично идентификатор равен предыдущий + 1
```
+++ market/idx/datacamp/proto/common/extension.proto

    // поля с данным триггером должны быть подмножеством полей с триггером miner_subscriber
    optional ESubscribeType miner_full_subscriber = 1701104;
+   optional ESubscribeType tatar_market_subscriber = 1701105;
}
```
#### Шаг 3
Добавляем конвертацию enum-значения из шага 1 в FieldOptions из шага 2 в [файл](https://a.yandex-team.ru/arcadia/market/idx/datacamp/lib/subscription/subscriber.cpp?rev=r9521622#L193)
```
+++ market/idx/datacamp/lib/subscription/subscriber.cpp

+  case Market::TATAR_MARKET_SUBSCRIBER:
+      return Market::tatar_market_subscriber;
```
#### Шаг 4
Размечаем нужные нам поля в [прото-схеме оффера](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r9405994#L41). Не стоит подписываться на все поля подряд, вы рискуете залить себя данными. 

Есть три вида подписки:
- ST_TRIGGER - при любых изменениях одного из полей данного типа в сторону подписчика отправится сигнал об изменении данных
- ST_SHIPMENT - дополнительные поля, которые добавляются в сообщение, отправляемое подписчику. При изменении только данных, помеченных этим тегом, сигнал в сторону подписчика не отправляется
- ST_EXISTENCE_TRIGGER - срабатывает на появление либо удаление поля, в случае с массивом не срабатывает на append в массив

{% note info %}

Поле `identifiers` отправляется в любом случае, нет необходимости в явной подписке на это поле.

{% endnote %}

{% note info %}

Для подписки на события создания новых офферов можно подписаться на поле `identifiers.offer_id` с типом `ST_TRIGGER`.

{% endnote %}

{% note info %}

Для подписки на события удаления офферов можно подписаться на поле `status.removed` с типом `ST_TRIGGER`.

{% endnote %}

Пример подписки на изменения любого из контентных полей оффера:
```
+++ market/idx/datacamp/proto/offer/DataCampOffer.proto 

   optional OfferContent          content          = 5 [
      (Market.miner_subscriber) = ST_SHIPMENT,
      (Market.turbo_subscriber) = ST_SHIPMENT,
+     (Market.tatar_market_subscriber) = ST_TRIGGER
```

#### Шаг 5
Создаем конфиг файл подписчика для диспатчера в [market/idx/datacamp/dispatcher/etc](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/etc?rev=r9521866).

```
+++ market/idx/datacamp/dispatcher/etc/tatar_market_sender.cfg

+ #include subscription_sender.cfg(Name='TatarMarketSubscriber', Subscriber='TATAR_MARKET_SUBSCRIBER', Color='WHITE,BLUE', UseActualServiceFields='true', OneServicePerUnitedOffer='false', Mode='MIXED', LBTopic=TATAR_MARKET_OUTPUT_TOPIC, LBWritersCount=${TATAR_MARKET_LOG_BROKER_OUTPUT_TOPIC_WRITERS_COUNT})
```

Описание параметров:
##### Name
Название вашего подписчика, обязательный параметр.

##### Subscriber
Тип вашего подписчика из шага 1, обязательный параметр.

##### ExportFormat
Формат сообщения, которое будет записано в топик, по-умолчанию `united`. Возможные значения:
* **united** — записывается [DatacampMessage](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/DatacampMessage.proto?rev=r9368860#L25), в котором заполняется поле `united_offers`
* **flat** — записывается [DatacampMessage](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/DatacampMessage.proto?rev=r9368860#L25), в котором заполняется поле `offers`. Каждый элемент это результат мерджа базового, сервисного и актуального сервисного частей
* **export** — записывается [ExportMessage](https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/api/ExportMessage.proto?rev=r9524383#L9), одно сообщение = один оффер, смердженный из трех частей
* **scope_filter** — записывается [DatacampOffer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r9368860#L41)
* **offer_history** — записывается [OfferHistory](https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/api/OfferHistory.proto?rev=r9524705#L12)

##### Color
Фильтрация офферов по их типу(цвету). По-умолчанию отправляются все офферы. Например `Color='WHITE;BLUE:vertical_approved'` выберет белые и заказанные товарной вертикалью синие офферы.

##### Mode
Фильтрация по наличию сервисной части, по-умолчанию `actual` Возможные значения:
* **actual** только офферы с актуальной сервисной частью
* **original** только офферы с сервисной частью
* **mixed** смешанный режим: офферы с сервисной частью, если нет актуальной

##### UseActualServiceFields
Для united формата этот флаг подразумевает, что актуальные части будут честно складываться в поле [actual](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/UnitedOffer.proto?rev=r8592849#L42), а не мержиться с сервисными.

##### OneServicePerUnitedOffer
Для united формата влияет на то, будет ли в united-оффере много сервисных частей или под каждую будет создан отдельные united оффер. Для новых подписчиков стоит ставить `false`

##### SamplingPercent
На этапе подключения вы можете подписаться на какой-то процент от всех событий обновления, пока не настроете партиции в логброкере либо настроите чтение со своей стороны. Число от 0 до 100, 0 — семплирование выключено и льется полный поток.

##### Остальное
Часть параметров остались в [коде](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/subscription_filter/config.h?rev=r9416286#L14), так как их настройка требует большей экспертизы в логике работы контроллеров. Вопросы можно задавать в чате офферного хранилища.

При добавлении кастомной логики фильтрации крайне желательно написать интеграционный тест в [market/idx/datacamp/dispatcher/tests](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/tests).

#### Шаг 6
Теперь надо добавить конфиг линки для нашего процессора в [market/idx/datacamp/dispatcher/etc](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/etc?rev=r9521866).

```
+++ market/idx/datacamp/dispatcher/etc/tatar_market_sender_links.cfg

+ #include subscription_sender_links.cfg(Name='TatarMarket', EnableDispatcherSubscription='true', DisableGatewaySubscription='true')
```

#### Шаг 7
Подключаем процессоры и линки из шага 5 и 6 в [market/idx/datacamp/dispatcher/etc/united.deploy.cfg](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/etc/united.deploy.cfg?rev=r9523483#L1).

```
+++ market/idx/datacamp/dispatcher/etc/united.deploy.cfg

    #include ${ENABLE_CVDUP_IMAGES_SENDER and ENABLE_CVDUP_IMAGES_SENDER=='true' and "cvdup_images_sender.cfg" or "empty.cfg"}
+   #include ${ENABLE_TATAR_MARKET_SENDER and ENABLE_TATAR_MARKET_SENDER=='true' and "tatar_market_sender.cfg" or "empty.cfg"}

....

    #include ${ENABLE_CVDUP_IMAGES_SENDER and ENABLE_CVDUP_IMAGES_SENDER=='true' and "cvdup_images_sender_links.cfg" or "empty.cfg"}
+   #include ${ENABLE_TATAR_MARKET_SENDER and ENABLE_TATAR_MARKET_SENDER=='true' and "tatar_market_sender_links.cfg" or "empty.cfg"}
```

#### Шаг 8
Настраиваем переменные окружения для тестинга, а конкретно название топика и флаг включения, в [market/idx/datacamp/dispatcher/etc/env/dispatcher.testing.united](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/etc/env/dispatcher.testing.united?rev=r9523483).

```
+++ market/idx/datacamp/dispatcher/etc/env/dispatcher.testing.united

+ ENABLE_TATAR_MARKET_SENDER=true
+ TATAR_MARKET_OUTPUT_TOPIC=tatar-market/testing/datacamp-offers
+ TATAR_MARKET_LOG_BROKER_OUTPUT_TOPIC_WRITERS_COUNT=1
```

#### Шаг 9
Настраиваем переменные окружения для прода в [market/idx/datacamp/dispatcher/etc/env/dispatcher.production.united](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/etc/env/dispatcher.production.united?rev=r9523483).

Правила хорошего тона гласят, что запись в продовые топики надо включать отдельным коммитом, уже после проверки всего пайплайна в тестинге.

```
+++ market/idx/datacamp/dispatcher/etc/env/dispatcher.production.united

+ ENABLE_TATAR_MARKET_SENDER=false
+ TATAR_MARKET_OUTPUT_TOPIC=tatar-market/prod/datacamp-offers
+ TATAR_MARKET_LOG_BROKER_OUTPUT_TOPIC_WRITERS_COUNT=1
```

#### Шаг 10
Поздравляю, осталось закоммитить изменения в аркадию и дождаться релиза [контроллеров](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-controllers).


### Версионированные поля { #versioned-fields }

Помимо прочего есть возможность логического объединения некоторой группы полей под некоторой версией. Как правило версия используется для двух таких кейсов:
- подписчик возвращает ответ в другом топике и надо понимать, актуален ли этот ответ (или данные, на которых он посчитан, старые)
- подписчик хочет иметь единое поле, в котором будет следить, поменялось ли какое-то другое из полей группы

Версионированные поля задаются через разметку в протобуфах. Пример:
- [счетчик версии](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r9414813#L425)
- [поля, влияющие на нее](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9414813#L523)


### Отправка данных в новом формате { #custom-format }

Помимо основных форматов есть возможность отправлять данные в логброкер в любом удобном вам виде. Для этого надо лишь написать код, переводящий данные оффера из United формата в ваш (например json или другой прото)

В качестве примера можно рассмотреть [обработчик](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/direct_search_snippet_moderation_sender/direct_search_snippet_moderation_sender.cpp?rev=r9165445#L89), конвертирующий отправляемые офферы в JSON. Не забудьте настроить [цепочку обработки](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/etc/direct_search_snippet_moderation_sender_links.cfg?rev=r9379839#L5) и [ее вершины](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dispatcher/etc/direct_search_snippet_moderation_sender.cfg?rev=r9379839#L9) в конфигах.
