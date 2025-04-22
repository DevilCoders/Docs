## Полезные ссылки
- [ITS datacamp](https://nanny.yandex-team.ru/ui/#/its/locations/market/datacamp/piper/)
- [Описание на Wiki](https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/datacamp-trouble-shooting/itsdatacamp/)
- [ITS Routines](https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/datacamp-trouble-shooting/itsdatacamp/#konfigurirovanieroutinescherezits)
- [ITS переопределение подписки](https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/datacamp-trouble-shooting/itsdatacamp/#pereopredeleniepodpiskicherezits)
- [История изменений](https://datacamp-admin.white.vs.market.yandex.net/its_history)
- [Построчный blame](https://datacamp-admin.white.vs.market.yandex.net/its_blame)

## Правила хорошего тона
- Перед(!) изменением конфигурации предупредить дежурного.
- Добавлять в комментарий ориентиры: номер тикета или кто/зачем добавил настройку. Это может выглядеть [вот так](https://paste.yandex-team.ru/5482292/text). 
- После изменения конфигурации убедиться, что всё продолжает работать (по графикам CPU, по графикам alive, по логам - на ваш вкус).

## Примеры неудачного использования
1. При использовании включения ваших процессоров в общий конфиг через #include важно понимать уязвимость: 
если "включающий" флаг переведен в false, в ITS не должно оставаться настроек для процессора, иначе мы получим невалидный конфиг, программа не запустится.
Подробнее неудачный сценарий можно изучить [на примере](https://paste.yandex-team.ru/5481099/text).

## Параметры процессоров
- **MaxInFlight** = количество одновременно обрабатываемых сущностей в одном контейнере контроллера или майнера
  - позволяет увеличить параллельность обработки в контроллерах
  - общий на все топики
  - может приводить к ООМ
  - соответствующая переменная окружения MAX_UNITED_OFFERS_INFLIGHT
  - пример: `"MAX_UNITED_OFFERS_INFLIGHT": "40000"`
- **MaxCount** = максимальное количество сообщений, которое процессор вычитывает из логброкера за один раз
  - это количество будет передано в Unpacker
  - пример: `"Proxy.Processors.MbocOfferStateUpdatesMytInput.MaxCount": "2"`
  - как правило, выставляется одновременно с MaxInProcess
  - внимание! устанавливать MaxCount=1 можно, только если вы уверены, что следующий процессор поддерживает MaxCount=1 (скорей всего это не так)
- **MaxInProcess** = количество сообщений, которое обрабатывается процессором
  - по умолчанию бесконечность
  - для пайпера и майнера сумма MaxInProcess по всем топикам в теории равна MaxInFlight
  - соответствующая переменная окружения LOG_BROKER_MAX_PROCESSING_MESSAGES
  - пример снижения количества коллизий: `"Proxy.Processors.MbocOfferStateUpdatesVlaInput.MaxInProcess": "1"`
  - как правило, выставляется одновременно с MaxCount
- **InfinityRetrySources** = список источников с бесконечными попытками записи в стейт
  - защищает от потери данных из указанного топика
  - увеличивает расход памяти и может приводить к ООМ
  - пример: `"Proxy.Processors.UnitedOffersUpdater.InfinityRetrySources": "DatacampMessageUnpacker"`
- **RetryCount** = количество попыток при записи в стейт
  - любая причина, включая коллизии транзакций, приводит к повторной попытке
  - [по умолчанию 20](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/initializer/config.h?rev=8161279&blame=true#L36_)
  - уменьшение увеличивает скорость разгребания топика и вероятность потери данных при коллизиях
  - распространяется на все данные в контроллере
  - пример: `"Proxy.Processors.Initializer.RetryCount": "1"`
- **AcceptedSources** = разрешение роутинга потока данных только от указанных источников
  - пример майнинга только от парсера: `"Proxy.Processors.UnitedMinerSender.AcceptedSources": "QOffersUnpacker"`
- **NotAcceptedSources** = запрет роутинга потока данных от указанных источников
  - позволяет убирать часть потока через фильтр
  - например, можно убрать поток в саас от майнера, добавив "MinerUnpacker"
  - пример выключения событийного майнинга: `"Proxy.Processors.UnitedMinerSender.NotAcceptedSources": "MinerUnpacker"`
  - пример выключения триггеров саас subsciptions_status и card_status (учитываем, что при отключении источника, отключаются все его триггеры): ```"Proxy.Processors.UnitedSaasFilter.NotAcceptedSources": "MinerUnpacker;MbocOfferStateUnpacker"```
- **IgnoreNotMinedOffers** = запрет отправки в саас новых офферов, не прошедших через майнер
  - специфичен для UnitedSaasDocsConverter
  - пример: `"Proxy.Processors.UnitedSaasDocsConverter.IgnoreNotMinedOffers": "true"`
- **IgnoreWhiteNotMinedOffers** = запрет отправки в саас новых офферов, не прошедших через майнер
  - применяется только к офферам, у которых все сервисные части белые. это позволит сохранить отправку в саас для синих, которые, не майнятся, пока не имеют актуальной части
  - специфичен для UnitedSaasDocsConverter
  - пример: `"Proxy.Processors.UnitedSaasDocsConverter.IgnoreWhiteNotMinedOffers": "true"`
- **Enabled** = выключение потока данных через процессор
  - пример выключения событийного майнинга: `"Proxy.Processors.UnitedMinerFilter.Enabled": "false"`

## Переменные окружения
- **DATACAMP_QOFFERS_INPUT_ENABLED и [аналогичные](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/env/qpiper.united)** = включает и выключает чтение топика
- [Список переменных](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/env/production.united)
- **API_IGNORED_PARTNERS**: позволяет задать список (плохих) бизнесов, для которых будут игнорироваться обновления API цен. `"API_IGNORED_PARTNERS": "1,2,3"`. стоит включать, если в топике market-quick копится лаг и есть подозрение, что проблема вызвана какими-то конкретными партнерами

## Пример
```
{
  "restart_service": true,
  "patches": {
    "Proxy.Processors.UnitedSaasDocsConverter.IgnoreNotMinedOffers": "true",
    "Proxy.Processors.MbocLbSender.NotAcceptedSources": "MbocOfferStateUnpacker",
    "Proxy.Processors.Initializer.RetryCount": "1",
    "Proxy.Processors.UnitedOffersUpdater.InfinityRetrySources": "DatacampMessageUnpacker",
    "Proxy.Processors.UnitedMinerFilter.Enabled": "false"
  },
  "env_conf": [
    {
      "file": "env/its.cfg",
      "values": {
        "CM_SENDER_ENABLED": "true",
        "OFFER_BIDS_INPUT_ENABLED": "true",
        "UNITED_MINER_INPUT_ENABLED": "true",
        "OFFERS_BLOG_INPUT_ENABLED": "false",
        
        "MAX_UNITED_OFFERS_INFLIGHT": "17000"
      }
    }
  ]
}
```
