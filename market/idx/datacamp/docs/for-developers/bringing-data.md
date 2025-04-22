# Поставка данных в статических табличках YT

# Поставка данных через logbroker

##  Создание топика

**Внимание!**
Если вы добавляете источник, через который офферы могут не только обновляться, но и создаваться, убедитесь, что этот источник перечислен в [CreateAllowedSources](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/offers_storage_updater.cfg?rev=r8892168#L20).

Данная процедура должна быть выполнена дважды - для testing и для prod
1. Идем в логброкер: https://lb.yandex-team.ru/
2. Находим нужную папку и создаем в ней топик. При создании топика указываем ABC, это раздаст нужные права
3. Идем в конфигурацию топика (вкладка *Configuration* слева) и добавляем необходимые TVM ключи
    - {% note tip %}

        Для быстрой настройки TVM можно использовать консольный клиент логброкера:
        ./logbroker -s logbroker permissions grant --path /logbroker-playground/folomkin/test-topic --subject 12345@tvm --permissions ReadTopic WriteTopic

    {% endnote %}

4. Там же указываем consumer для топика
5. Настраиваем мониторинги и алерты для метрик с logbroker на [Соломоне](https://solomon.yandex-team.ru/admin/projects/market.datacamp).
У вас должны быть права на изменения
6. Если вы неуверены, что вам нужен отдельный канал в соломоне, используйте общий [juggler-default](https://solomon.yandex-team.ru/admin/projects/market.datacamp/channels/juggler-default)
7. Используя созданные каналы, заводим алерты.
    - {% note tip %}

        Для быстрого создания каналов настройки можно использовать [скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/create_solomon_alerts)

    {% endnote %}

На кaждый топик создается как минимум три алерта для следующих метрик:
- *CreateTimeLagMsByCommitted*
- *MessageLagByCommitted*
- *ReadTimeLagMs*
Для быстрой настройки так же можно найти алерт для других топиков piper и дублировать их.

Эти же метрики следует добавить на дашбоард piper в соответствующие [разделы](https://solomon.yandex-team.ru/admin/projects/market.datacamp/dashboards?text=piper).
Если все выполнено правильно - должны отобразиться графики.
Чтобы они были не пустыми - можно выполнить запись через консольный клиент логброкер.

Далее следует подключить каналы в juggler.

Идем [сюда](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs/configs/mi-datacamp-united.yaml) и добавляем хосты из наших каналов в соответствующие секции:
- *CreateTimeLagMsByCommitted* -> piper-lb-commit-time-lag
- *MessageLagByCommitted* -> piper-lb-read-time-lag
- *ReadTimeLagMs* -> piper-lb-length

### Настройка logfeller
Для топика выполнить настройку logfeller по следующей [инструкции](https://wiki.yandex-team.ru/logfeller/connection/).

### Создание конфигурации piper
Piper работает на основе фреймворка common proxy.

Настроенные топики добавляем в следующие [файлы](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/):

*testing.united*
```ini
DATACAMP_TEST_INPUT=/path/to/topic
DATACAMP_TEST_ENABLE=true
```

*prod.united*
```ini
DATACAMP_TEST_INPUT=/path/to/topic
DATACAMP_TEST_ENABLE=false
```

*qpiper.united*
```ini
DATACAMP_TEST_ENABLE=false
```
Желательно объединять их в группы по общим признакам.

Далее, идем в папку конфигурациии выбранного контроллера.
Для piper, например, это https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/piper/etc

Создаем пару файлов - для процессоров и для соединяющих их линков.

*my_processors.cfg*
```ini
#include lb_reader.cfg(Name='DatacampCategories', Topic=DATACAMP_TEST_INPUT, MessageType='DatacampMessage', CommitOnFail='false', BatchSize=1, InputEnabled='${DATACAMP_TEST_ENABLE or true}')

<TestUnpacker>
    Type: DATACAMP_MESSAGE_UNPACKER
    OutputBatchSize: ${BATCH_SIZE or 100}
    MaxInFlight: ${MAX_UNITED_OFFERS_INFLIGHT}
</TestUnpacker>
```
В качестве type указываем тип выбранного процессора.
Также задаем дополнительные опции.

*my_links.cfg*

```ini
#include lb_reader_links.cfg(From='DatacampCategories', To='CategoriesUnitedUnpacker')

<Link>
    From: CategoriesUnitedUnpacker
    To: DatacampMessageToCategoryConverter
</Link>
```
Линк будет передавать от процессора распаковщика данные в выбранный процессор.
В файле *united.cfg* включаем через директиву **#include** созданные файлы.

### Управление конфигурацией в деплое
Чтобы не потерять существующие данные, следует сначала включить чтение и запись в топик в правильной последовательности.
Например, если данные уже идут в другом топике, и вы переключаете поток, то в начале следует включить запись в топик, а потом уже чтение.

Для оперативного управления включением и выключением топиками следует использовать ранее созданные флаги.
В деплое их можно задавать [здесь](https://nanny.yandex-team.ru/ui/#/its/locations/market/datacamp/piper/).
