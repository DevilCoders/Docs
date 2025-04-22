# Pricechecker

## Эксплуатация

### Логи pricechecker

Логи pricechecker поставляются в YT с помощью [Unified Agent](https://wiki.yandex-team.ru/logbroker/unified-agent/).
Конфигурация поставки логов лежит в конфиге unified agent:

- [Прод](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/prod/pricechecker_unified_agent.yml)
- [Тестинг](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/testing/pricechecker_unified_agent.yml)

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
            <td rowspan=2>Лог запросов к pricechecker</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/pricechecker/proto/reqans_logrecord.proto">TReqAnsLogRecord</a></td>
            <td rowspan=2>pricechecker-reqans.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/hotels-pricechecker-log">/travel/prod/hotels-pricechecker-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-pricechecker-log.json">travel-hotels-pricechecker-log</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L142">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-hotels-pricechecker-log&">//logs/travel-prod-hotels-pricechecker-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-pricechecker-log">/travel/test/hotels-pricechecker-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-pricechecker-log&">//logs/travel-test-hotels-pricechecker-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Логи результатов проверки цен</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/pricechecker/proto/pricechecker_logrecord.proto">TPriceCheckerLogRecord</a></td>
            <td rowspan=2>pricechecker-tracking-results.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/hotels-pricechecker-results">/travel/prod/hotels-pricechecker-results</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-hotels-pricechecker-results.json">travel-hotels-pricechecker-results</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L147">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-hotels-pricechecker-results&">//logs/travel-prod-hotels-pricechecker-results</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/hotels-pricechecker-results">/travel/test/hotels-pricechecker-results</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-hotels-pricechecker-results&">//logs/travel-test-hotels-pricechecker-results</a></td>
        </tr>
    </tbody>
</table>

**<a name="dagger">†</a>** Конфигурация сгенерированна по .proto описанию с помощью [gen_logfeller_parser](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser).
