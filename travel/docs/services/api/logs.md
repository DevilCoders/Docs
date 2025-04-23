---
title: Логи Travel-API
rank: 90
---

### Логи Travel-API

Логи API поставляются в YT с помощью [push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client/).
Сейчас такой способ поставки признан устаревшим. 
В будущем необходимо будет выполнить переход на [Unified Agent](https://logbroker.yandex-team.ru/docs/unified_agent/).
Тикет для переезда [TRAVELBACK-382](https://st.yandex-team.ru/TRAVELBACK-382).


Конфигурация поставки логов лежит в конфиге push_client:

- [Прод](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/prod/api_push_config.yaml)
- [Тестинг](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/testing/api_push_config.yaml)

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
            <td rowspan=2>Исходящие http запросы</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/java/commons/src/main/java/ru/yandex/travel/commons/logging/LogEventRequest.java">LogEventRequest</a></td>
            <td rowspan=2>http-results.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/api-partners-http-log">/travel/prod/api-partners-http-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-api-partners-http-log.json">travel-api-partners-http-log</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-api-partners-http-log&">//logs/travel-prod-api-partners-http-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/api-partners-http-log">/travel/test/api-partners-http-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-api-partners-http-log&">//logs/travel-test-api-partners-http-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Входящие http запросы</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/java/spring-boot-skeleton/src/main/java/ru/yandex/travel/http/ReqAnsLoggerInterceptor.java?rev=6790033#L80">ReqAnsEvent</a></td>
            <td rowspan=2>req-ans.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/api-reqans-log">/travel/prod/api-reqans-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-api-reqans-log.json">travel-api-reqans-log</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-api-reqans-log&">//logs/travel-prod-api-reqans-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/api-reqans-log">/travel/test/api-reqans-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-api-reqans-log&">//logs/travel-test-api-reqans-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Логи приложения</td>
            <td rowspan=2>-</td>
            <td rowspan=2>api.log.json </td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/api-application-log">/travel/prod/api-application-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-api-application-log.json">travel-api-application-log</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-api-application-log&">//logs/travel-prod-api-application-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/api-application-log">/travel/test/api-application-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-api-application-log&">//logs/travel-test-api-application-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Логи показов саджеста отелей</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/api/proto/hotels_suggest.proto">THotelsSuggestLogRecord</a></td>
            <td rowspan=2>suggest.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/api-hotels-suggest-log">/travel/prod/api-hotels-suggest-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-api-hotels-suggest-log.json">travel-api-hotels-suggest-log</a> (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-api-hotels-suggest-log&">//logs/travel-prod-api-hotels-suggest-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/api-hotels-suggest-log">/travel/test/api-hotels-suggest-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-api-hotels-suggest-log&">//logs/travel-test-api-hotels-suggest-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Логи выбора саджеста пользователем</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/api/proto/hotels_suggest.proto">THotelsSuggestChoiceLogRecord</a></td>
            <td rowspan=2>suggest-choice.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/api-hotels-suggest-choice-log">/travel/prod/api-hotels-suggest-choice-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-api-hotels-suggest-choice-log.json">travel-api-hotels-suggest-log</a> (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-api-hotels-suggest-choice-log&">//logs/travel-prod-api-hotels-suggest-choice-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/api-hotels-suggest-choice-log">/travel/test/api-hotels-suggest-choice-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-api-hotels-suggest-choice-log&">//logs/travel-test-api-hotels-suggest-choice-log</a></td>
        </tr>
    </tbody>
</table>

**<a name="dagger">†</a>** Парсеры, помеченные как `generated` сгенерированы с помощью тулзы [gen_logfeller_parser](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser)
