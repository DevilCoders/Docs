# Турбоапп в заказах через КЦ

## Задача
Для заказов через колцентр (ППЗ и другие каналы, использующие только смс/звонки для связи с пассажиром) хотим отправлять СМС со ссылкой на заход в турбоапп для этого заказа. В турбоаппе предлагается авторизоваться. В зависимости от авторизованности для пользователя заказ будет либо отображаться как обычный с полной функциональностью ТА, либо только с урезанным функционалом.  
Для оптимизации отправки СМС хочется понимать открыл ли пользователь ссылку в СМС или нет  
https://st.yandex-team.ru/TAXIBACKEND-35084

## Реализация

Необходимо реализовать: отправку СМС с ссылкой на ТА, на фронте ТА работу с ссылкой и интерфейс с урезанной функциональностью для неавторизованных (и авторизованных под другим телефоном) пользователей, на бэке взаимодействие со своими заказами из КЦ, отслеживание открытия ТА по СМС, остановку отправки СМС при открытии ссылки

### Соображения безопасности
[С безопасниками договорились](https://st.yandex-team.ru/TAXIPROJECTS-2134#60781572096a67785c578744), что авторизованным по тому же номера телефона пользователям можно будет доступна полная функциональность ТА, а неавторизованным (и авторизованным с другим номером телефона) - урезанная: только отмена.  
Для управления и просмотра заказа его нужно сначала получить, для этого нужен какой-то его идентификатор  
С точки зрения безопасноти, нехорошо отдавать в СМС ссылку с order_id: перехватившие её злоумышленики могут попробовать подёргать ручки заказа, если в каких-то будет дыра - смогут управлять заказом.  
Альтернатива order_id - route_sharing_key (ключ, который используется в функции "поделиться заказом"), он связан 1к1 с order_id, имеет ограниченное время жизни и сейчас не используется для управления заказом, поэтому при перехвате даст доступ только к урезанной функиональности неавторизованного пользователя. Однако, если пользователь не захочет авторизоваться, а потом поделиться заказом с кем-нибудь с помощью функции "поделиться заказом" мы не сможем (без доп. доработок) отличать владельца от того, кому он отдал ссылку

### Отправка СМС
СМС будет в себе содержать [укороченную](https://github.yandex-team.ru/taxi/backend-py3/blob/f2dda6eea3cdd3d5672dffd21cca2cec15cc34ae/schemas/services/ya-cc/api/yacc.yaml#L33) ссылку на ТА + параметры необходимые для отображения заказа  
 
Параметр route_sharing_key - нужно доработать orders/search, чтобы работал с ним  
Для того, чтобы отличить владельца от того, с кем ключом просто поделились можно:  
1. дополнительно передавать какой-то bool флаг, типа is_owner/show_extended_ui (плохое решение)
1. завести новый ключ для шарилки owner_sharing_key, таким образом владение заказом можно будет проверять на бэке
1. ничего не делать, считать сценарий "заказ в КЦ, которым поделился неавторизованный пользователь" редким и не критичным. Но на бэке проверять application заказа и сверять его с конфигом приложений, для которых можно управлять заказом с помощью rsk

ЛИБО

4. Отдавать order_id и считать, что в этом нет ничего страшного

На мой взгляд предпочтительный вариант - 3й

Места отправки СМС:  
1. КЦ (callcenter) https://github.yandex-team.ru/taxi/uservices/blob/ae7887ea40ad0520f6bfdc6dac2d7e9ec5ffb734/services/ivr-dispatcher/src/stq/notification_processor/notification_processor.cpp#L367  
1. ППЗ (Продажа парковых заказов) https://github.yandex-team.ru/taxi/backend/blob/b4c017d9974883a55d58f2e659e0980882eb6e34/taxi/internal/notifications/order/\_\_init\_\_.py#L134
1. КК (корп. кабинет) TODO

### Прорастание заказов в Турбоапп
Для авторизованных пользователей.  
Заказы должны прорастать автоматически, даже если пользователь откроет турбоапп не по ссылке. Список заказов, которые отображаются в ТА приходит из руки startup. Для того, чтобы в ней приходили заказы КЦ нужны доработки в order-core в ручке [active-orders](https://github.yandex-team.ru/taxi/uservices/blob/c4784970c1c99f65864887ce4f32592e2887a2c4/services/order-core/docs/yaml/api/external-api.yaml#L100) (из неё [startup](https://github.yandex-team.ru/taxi/api-proxy-config/blob/0e296f4c2859ab04e23ab8278de87e211fea13b9/default/endpoints/4-0-startup/post.yaml#L47) берёт заказы). Ручка должна возвращать заказы из КЦ (КК/ППЗ настриваемо конфигом) с тем же phone_id.  

Конфиг BRAND_TO_CONTROLLERD_APPS_MAPPING  
```yaml
description: Маппинг из бренда в список приложений, заказами в которых пользователь может управлять (при наличии связи по phone_id)
default:
    __default__: []
    turboapp: [call_center]
schema:
    type: object
    additionalProperties:
        $ref: '#/definitions/SearchedApplications'
    required:
      - __default__
    properties:
        __default__:
            $ref: '#/definitions/SearchedApplications'

    definitions:
        SearchedApplications:
            description: |
                Искать заказы с одним из этих приложений
            type: array
            items: string
                    
```
[Вот здесь](https://github.yandex-team.ru/taxi/uservices/blob/78e92231dfc62ff44a1cdfb554a363078ecd1715/services/order-core/src/models/active_orders_proc.cpp#L131) добавить условие: если бренд есть в конфиге и для него значение не пустой массив, то ищем заказы не только по user_id/yandex_uid, но и по phone_id + application - из массива SearchedApplications

Кроме того, нужно будет проверить, что route_sharing_key совпадает с тем, что пришёл в заказе (нужно возвращать rsk в search)  
Необходимы доработки ручек int-api позволяющие пользователю взаимодействовать со своим заказом из КЦ:
- cancel, [click](https://github.yandex-team.ru/taxi/backend-cpp/blob/b27ffe702f37a0dcf76fd9bdf269a5d7150cc21d/protocol/lib/src/orderkit/order_canceller.cpp#L165)
- changedestinations, [click](https://github.yandex-team.ru/taxi/backend-cpp/blob/7b18adc113ec3f4ce8f52aeda0bb4f5b31698e76/protocol/lib/src/views/changedestinations.cpp#L324)
- changepayment, не требуется
- search, не требуется

Для пользователей неавторизованных и авторизованных под другим номером телефона.  
В этом случае в startup order_id не придёт, и нужно использовать переданный route_sharing_key.  
Необходимо на фронте дёргать ручки /4.0/sharedroute/info, /4.0/sharedroute/track и отрисовывать полученные из них данные. Т.к. внешний вид для авторизованного и неавторихованного пользователей будут сильно отличаться, лучше отрисовывать полученные данные на новой странице/представлении. Обязательно не забыть показать на этой странице баннер предлагающий установить Yandex GO как на саммари в турбоаппе  
Нужно будет доработать /4.0/sharedroute/info, чтобы возвращала флаг, показывающий может ли пользователь отменить заказ  
Дорабатываем cancel, чтобы он мог работать с rsk для неавторизованных пользователей и заказов из КЦ (точнее заказов с приложением из конфига выше)

### Переход с СМС на пуши
Хочется уметь понимать, что пользователь открыл ссылку, зашёл в ТА и разрешил пуши, чтобы иметь возможность перейти с СМС на пуши в ТА  
Определять что ссылка открыта можно по вызову orders/search с route_sharing_key и тому, что application в конфиге (ставить stq, которая будет сохранять событие вызова)
Информацию о том, что ссылку открыли можно хранить в бд user-state. 

```sql
CREATE TYPE user_events.event_type AS ENUM ('turboapp_opened');

CREATE TABLE user_events.user_events (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  order_id TEXT NOT NULL,
  user_events.event_type NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```
В рамках нашей задачи информация о заходе нужна только на время поездки, поэтому стоит настроить чистку БД с помощью сервиса архивации

После с обсуждением с менеджером решили, что отслеживание захода по ссылке будем делать после MVP. На время MVP достаточно механизма ниже

Включение пушей в турбоаппе происходит вызовом [ucommunications/user/notification/subscribe](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/ucommunications/docs/yaml/api/user_notification_subscribe.yaml#L13) в [startup'е](https://github.yandex-team.ru/taxi/api-proxy-config/blob/0e296f4c2859ab04e23ab8278de87e211fea13b9/default/endpoints/4-0-startup/post.yaml#L330), user_id и нужные для пушей данные сохраняются в монго.  
В сервисе ucommunication есть возможность автоматически отправлять пуши вместо СМС. Для этого необходимо с фронта отрпавлять [acknowledgement](https://wiki.yandex-team.ru/taxi/backend/architecture/communications/client-push/#upravlenieacknowledgepushejj), добавить настройки этой фичи для intent'а СМС в [конфиг](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/COMMUNICATIONS_SMS_INTENTS_MAP?name=COMMUNICATIONS_SMS_INTENTS_MAP) и в ручку отправки смс передавать объект [notification](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/ucommunications/docs/yaml/api/user_sms_send.yaml#L154)

## Итого
MVP:
1. Доработать order-core, чтобы возвращал заказы связанные по phone_id 2d
1. Доработать orders/search, чтобы возвращал route_sharing_key 1d
1. Доработать sharedroute/info, чтобы возвращал флаг can_cancel 1d
1. Доработать orders/cancel, чтобы отменял заказы по route_sharing_key 1d
1. Доработать changedestinations и cancel, чтобы обрабатывали запросы от пользователя с другим user_id, но тем же phone_id 3d
1. В ivr-dispatcher отправлять СМС с ссылкой на турбоапп и route_sharing_key в параметрах 3d
1. Настроить фичу "пуши вместо СМС" для описанного сценария 2d

~13d на backend


На потом:
1. Завести БД, в которой сохранять событие захода в турбоапп по ссылке. stq на сохранение, ручка на проверку того, что для пользователя событие есть
1. Отправлять ссылку в смс для ППЗ
1. Отправлять пуши вместо смс ППЗ
1. Отправлять ссылке в смс для КК 
1. Отправлять пуши вместо смс КК
