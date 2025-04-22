# Redir

## Эксплуатация

### Логи redir

Логи redir поставляются в YT с помощью [Unified Agent](https://wiki.yandex-team.ru/logbroker/unified-agent/).
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
            <td rowspan=2>Лог запросов к redir, отели</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/redir/proto/reqans_hotels.proto">TReqAnsLogRecord</a></td>
            <td rowspan=2>redir_reqans.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel-redir/travel-redir-log">/travel-redir/travel-redir-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-redir-log.json">travel-redir-log</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L152">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-redir-log&">//logs/travel-redir-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/redir-log">/travel/test/redir-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-redir-log&">//logs/travel-test-redir-log</a></td>
        </tr>
        <tr>
            <td rowspan=2>Лог запросов к redir, поезда</td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/redir/proto/reqans_trains.proto">TReqAnsLogRecord</a></td>
            <td rowspan=2>redir-reqans-trains.log</td>
            <td>Прод: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/prod/redir-trains-log">/travel/prod/redir-trains-log</a></td>
            <td rowspan=2><a href="https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/travel-redir-trains-log.json">travel-redir-log</a>  (<a href="https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser/main.cpp?rev=6856863#L157">generated</a>)<a href="#dagger">†</a></td>
            <td>Прод: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-prod-redir-trains-log&">//logs/travel-prod-redir-trains-log</a></td>
        </tr>
        <tr>
            <td>Тестинг: <a href="https://lb.yandex-team.ru/logbroker/accounts/travel/test/redir-trains-log">/travel/test/redir-trains-log</a></td>
            <td>Тестинг: <a href="https://yt.yandex-team.ru/hahn/navigation?path=//logs/travel-test-redir-trains-log&">//logs/travel-test-redir-trains-log</a></td>
        </tr>
    </tbody>
</table>

**<a name="dagger">†</a>** Конфигурация сгенерированна по .proto описанию с помощью [gen_logfeller_parser](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/gen_logfeller_parser).
