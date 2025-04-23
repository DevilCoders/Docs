# Searcher

Ищет офферы у партнеров.
[Описание на Wiki](https://wiki.yandex-team.ru/travel/hotels/dev/services/searcher/).


## Как сделать запрос

Для запросов к searcher с целью тестирования можно использовать [searcher_client](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/searcher_client).


## Эксплуатация

### Gracefull restart

На локальной машине необходимо выполнить:

```
curl -X POST localhost:8080/actuator/shutdown
```

### Логи searcher

Логи searcher'а поставляются в YT с помощью [push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client/).
Сейчас такой способ поставки признан устаревшим. 
В будущем необходимо будет выполнить переход на [Unified Agent](https://logbroker.yandex-team.ru/docs/unified_agent/).
Тикет для переезда [TRAVELBACK-382](https://st.yandex-team.ru/TRAVELBACK-382).

Конфигурация поставки логов лежит в конфиге push_client:

- [Прод](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/prod/searcher_push_config.yaml)
- [Тестинг](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/testing/searcher_push_config.yaml)

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
            <td rowspan=2>Результат поиска</td>
            <td rowspan=2>-</td>
            <td rowspan=2>search-results.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel-hotels-searcher/search-result-log">/travel-hotels-searcher/search-result-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-search-result-log.json">travel-hotels-search-result-log</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-hotels-search-result-log&">//logs/travel-hotels-search-result-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-search-result-log">/travel/test/hotels-search-result-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-search-result-log&">//logs/travel-test-hotels-search-result-log/</a></td>
        </tr>
        <tr>
            <td rowspan=2>Лог http-запросов к партнерам (старый лог, который используется для логирования запросов к некоторым партнерам)</td>
            <td rowspan=2></td>
            <td rowspan=2>http-results.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel-hotels-searcher/http-log">/travel-hotels-searcher/http-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-searcher-http-log.json">travel-hotels-searcher-http-log</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-hotels-searcher-http-log&">//logs/travel-hotels-searcher-http-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-searcher-http-log">/travel/test/hotels-searcher-http-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-searcher-http-log&">//logs/travel-test-hotels-searcher-http-log</a></td>
        </tr>
        <tr>
            <td>Лог приложения</td>
            <td>-</td>
            <td>searcher.log</td>
            <td>-</td>
            <td>-</td>
            <td>-</td>
        </tr>
        <tr>
            <td rowspan=2>Лог приложения в JSON формате</td>
            <td rowspan=2>-</td>
            <td rowspan=2>searcher.log.json</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel-hotels-searcher/application-log">/travel-hotels-searcher/application-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-searcher-application-log.json">travel-hotels-searcher-application-log</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-hotels-searcher-application-log&">//logs/travel-hotels-searcher-application-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-searcher-application-log">/travel/test/hotels-searcher-application-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-searcher-application-log&">//logs/travel-test-hotels-searcher-application-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Лог катрум событий</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/searcher/proto/catroom_eventlog_record.proto">TCatroomEventLogRecord</a></td>
            <td rowspan=2>catroom-event-log.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/hotels-catroom-eventlog">/travel/prod/hotels-catroom-eventlog</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-catroom-eventlog.json">travel-hotels-catroom-eventlog</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L160">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-hotels-catroom-eventlog&">//logs/travel-prod-hotels-catroom-eventlog</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-catroom-eventlog">/travel/test/hotels-catroom-eventlog</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-catroom-eventlog&">//logs/travel-test-hotels-catroom-eventlog</a></td>
        </tr>
        <tr>
            <td rowspan=2>Лог http-запросов к партнерам</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/java/commons/src/main/java/ru/yandex/travel/commons/logging/LogEventRequest.java">LogEventRequest</a></td>
            <td rowspan=2>hotels-searcher-partners-http-log.json</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/hotels-searcher-partners-http-log">/travel/prod/hotels-searcher-partners-http-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-searcher-partners-http-log.json">travel-hotels-searcher-partners-http-log</td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-hotels-searcher-partners-http-log&">//logs/travel-prod-hotels-searcher-partners-http-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-searcher-partners-http-log">/travel/test/hotels-searcher-partners-http-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-searcher-partners-http-log&">//logs/travel-test-hotels-searcher-partners-http-log</a></td>
        </tr>
    </tbody>
</table>

**<a name="dagger">†</a>** Конфигурация сгенерированна по .proto описанию с помощью [gen_logfeller_parser](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser).
