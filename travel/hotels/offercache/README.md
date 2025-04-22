# Offercache

Кэш офферов отелей

## Правила обработки офферов

* [SearchInCache]
  * Выбираем ключ (Date/Nights/Ages) для ответа
  * Получаем все офферы по ключу

* [PutRecordsToResp]
  * [GetAllVisibleOffers]
    * Выкидываем офферы отключенных операторов. SR_OperatorDisabled.
    * В случае Exp=4011 выкидываем офферы Expedia без бесплатной отмены. SR_Exp4011.
    * В случае если не Exp=4460 выкидываем офферы на несколько комнат, если каждая - на одного взрослого. SR_Multiroom4460
    * В случае если не Exp=4471 выкидываем офферы на несколько комнат, если каждая - на несколько взрослых. SR_Multiroom4471.
    * Между TL, Dolphin & Expedia выбираем только одного оператора по правилам HOTELS-4408. SR_OtherBoYOperatorWon.
  * [ScanPermaroom]
    * Если Full=1 и текущий пермалинк - главный, то смотрим на пермарумы.
    * Пермарумы сортируем по цене минимального оффера в каждом пермаруме, а other - в конце
  * Выкидываем офферы, относящиеся к скрытому пермаруму, а так же к other, если он не показывается (для этого пермалинка)
  * [PutFilterSetsToHotel]
    * Формируем список доступных пользовательских фильтров
  * [FilterOffers]
    * Фильтруем офферы по пользовательским фильтрам
  * [ReduceOffersByOperator]
    * Если Full=0 - оставляем по одному офферу от каждой группы (по оператору или пермаруму)
  * [SortOffers]
    * Сортируем офферы
  * Если пермалинк - не главный, оставляем только один - первый - оффер
  * [BumpOffers]
    * Если пермалинк - главный, то на первое место выносим по одному (минимальному) офферу от bumped операторов
  * Формируем ответ

__Проблема__:

При установке PriceFrom можем отфильтровать единственный оффер выжившего BoY
Аналогично при выкидывании скрытых офферов при катруме.

Предложение
1. Выкидываем отключенных операторов
2. Эксперименты 4011,4460,4471
3. Катрумизируем. Выкидываем скрытые офферы. И офферы "прочие", если надо и катрумизация удалась
4. Применяем фильтр по цене
5. Выбираем BoY оператора
6. Сокращаем если Full=0
7. Если Full=1, формируем доступные пользовательские фильтры
8. Применяем пользовательские фильтры
9. Сортируем офферы
10. Bump


## Эксплуатация

### Логи offercache

Логи offercache поставляются в YT с помощью [Unified Agent](https://wiki.yandex-team.ru/logbroker/unified-agent/).
Конфигурация поставки логов лежит в конфиге unified agent:

- [Прод](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/prod/offercache_unified_agent.yml)
- [Тестинг](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/testing/offercache_unified_agent.yml)

**Логи:**

<table>
    <thead>
        <tr>
            <th>Лог</th>
            <th>Схема</th>
            <th>Файл</th>
            <th>Топик</th>
            <th>Парсер</th>
            <th>YT</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=2>Лог запросов к offercache</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/offercache/proto/reqans_logrecord.proto">TReqAnsLogRecord</a></td>
            <td rowspan=2>reqans_offercache.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/travel-hotels-offercache-log">/travel/travel-hotels-offercache-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-offercache-log.json">travel-hotels-offercache-log</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L127">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-hotels-offercache-log&">//logs/travel-hotels-offercache-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-offercache-log">/travel/test/hotels-offercache-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-offercache-log&">//logs/travel-test-hotels-offercache-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Лог запросов к offercache по протоколу GRPC</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/offercache/proto/grpc_reqans_logrecord.proto">TGrpcReqAnsLogRecord</a></td>
            <td rowspan=2>grpc_reqans_offercache.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/hotels-offercache-grpc-reqans-log">/travel/prod/hotels-offercache-grpc-reqans-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-offercache-grpc-reqans-log.json">travel-hotels-offercache-grpc-reqans-log</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L130">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-hotels-offercache-grpc-reqans-log&">//logs/travel-prod-hotels-offercache-grpc-reqans-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-offercache-grpc-reqans-log">/travel/test/hotels-offercache-grpc-reqans-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-offercache-grpc-reqans-log&">//logs/travel-test-hotels-offercache-grpc-reqans-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Лог использования кэша в offercache</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/offercache/proto/cacheusage_logrecord.proto">TCacheUsageLogRecord</a></td>
            <td rowspan=2>cacheusage_offercache.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/hotels-offercache-cacheusage-log">/travel/prod/hotels-offercache-cacheusage-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-offercache-cacheusage-log.json">travel-hotels-offercache-cacheusage-log</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L137">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-hotels-offercache-cacheusage-log&">//logs/travel-prod-hotels-offercache-cacheusage-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-offercache-cacheusage-log">/travel/test/hotels-offercache-cacheusage-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-offercache-cacheusage-log&">//logs/travel-test-hotels-offercache-cacheusage-log</a></td>
        </tr>
    </tbody>
</table>

**<a name="dagger">†</a>** Конфигурация сгенерированна по .proto описанию с помощью [gen_logfeller_parser](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser).
