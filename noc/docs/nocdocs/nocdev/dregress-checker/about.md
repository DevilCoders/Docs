# Документация о сервисе Dr.Egress - Checker
Dr.Egress - Checker - сервис по обработке метрик мониторинга dregress'а, выявления проблем на стыках/AS и составление обходных маршрутов.

## Схема работы
[drawio](https://drawio.yandex-team.ru?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=dregress.drawio#R7VxZk9o4EP411O4%2BkPIl2zzCwGS3MltJ7eyVfTOgAScGEWMC5NevZEm2bMlg8MUck5TLlnV299ctdbfpmXerw%2FvQ2yx%2FR3MY9AxtfuiZ455huI6Nr6TgyAsMWrAI%2FTkt0tOCR%2F8HZIUaK935c7jNVIwQCiJ%2Fky2cofUazqJMmReGaJ%2Bt9oSC7KgbbwGlgseZF8il%2F%2FjzaMlWYThp%2Ba%2FQXyz5yLo9oG9WHq%2FMVrJdenO0F4rMSc%2B8CxGK6N3qcAcDQjtOF9ruvuBtMrEQrqMyDcbaX%2F%2F1v337Mfi0%2F3u1fx98%2BbD%2Fo29btJvvXrBjK2azjY6cBCHareeQ9KL3zNF%2B6UfwcePNyNs95jkuW0argL1%2B8oPgDgUojNuacwDduYXLt1GIvkLhjWtMTdvGb7xwxtiOSTJi04FhBA%2BFC9UT8mGxg2gFo%2FCIq7AGls5YcOQ80RgL9ikHMQtp2VLgnmWzih6TmkXSeUpYfMNoewmdNYmscI4FjT2iMFqiBVp7wSQtHaWE1%2FBTWucBoQ0j9xcYRUdGPm8XoSwzsMhtyJunAB6GBAwJgcngp8mL54p24QyeWBQw1HwIYeBF%2FvfsACqSsqafkI%2BHTvgHOLE4%2FzQrx5bICxcwYs1ynEnmcT2zgPHyQIH7zhDVNkpiwswTvzZMAF2iaguYgAc%2F%2Bpc0fwfY02fhzfjAeo4fjvxhjdcrNCKPn8V3abP4ibdrGH%2FWoBH8mU5Wf4K8VmwYftbg5cNPtzuHH5%2BRQOYoxHfPBJM14shkJKZyfaqiUxFw1RimybjApBhq5DoCPUwwLEHkSkvodRyX6PH9XXx1eU18P4mvuFc7wAsfTUN8tyB3OugZ%2BL%2FGWrAbXWg04sPGVwmgS7Sa7rbnwVkDuEwju2EwFODSeR0RXElh%2FbyyXiOO%2BAHtHI6sqhvHarzRFfaFyv92460zXLO%2F7cj5jApxf0uleIirrFG48oK0AscNgcPAEfB3LyBywrDI0ESJGqAVWsed0jngNdFpsA4FaFaaWL1LvM9qArwsM76KSwdM6RhFlLCFamOmlUjlpFpFpZZUjhuyxxGvn7wa8p5xD6CQDYU7EK0VJWe4WSXnKjYQmkLHNXakNR2lOaom%2FKkBukrKciJwT7xI2vBRkMD4HXscir332azoIHVK4Y0JjqU6%2BbUqOZb9XIzjtQe%2FGo2qZZTdnGpqMWjHqPJpNmdULUEL3GchTO%2BpNbEE8JlZvBdr%2FhPWNyeo%2FEi%2FCdEMbkvsb6fe7OsiFt6Puyjw17BGZFs5R5nKJrgKZDfn0ulk21sebWdBBMyKICrnUrG1HAeoGmjOo9mJxq1RC1K%2BlGEg6FIL8mnelBYc0D3QM9VxZg45Vuc6TnZPvlK%2FGQBlQel2Ckogg%2FLNb0asUi5Q6ihOBi37zexnczSocdNhV7VZZeOobsu7DjnCINiwiYAM7hLIwAxfE99R4hfShYO8K5RMmCHs%2FLSd2%2Bm5nftpbNkFcR5SqsjlLe0H7QIudJV6gGnkHYVqG1JhWzyQo%2BUH0nLZO2dnlm2Ab%2BgcakWwrXCVX%2BjjG48K3XvDs2AW3XYjYQQgNAE90cXHZ5bz%2BKV9i%2BbXElwBLjfIWnyMFrUN4Jts6n9MmsiH3ba1jZ0To%2B61jXONtnmtvj277AbaqaruqlkQxQb6Jk61J7XDCzj8Jq76JJNRmbXV5unXVkR9apWFEkaBaPvLmDk7YsbMYViCm1QVPUzb8G3kIjNAlRSk0t7NcVexY2%2BbuxeY%2FJcgBFbhlrMzKXDNLmw4zcbjSfZ1nxcGJS0tzcHrzNIqUh8JaoAABHGn7ea2rifDXIk3Sra2%2BGYsebeY6WwRTlkZSj6YIA%2BLwCPGOL6foZU%2Fy%2BzGqiEw52LWTcUuWtf0FnfRbidxtEYR6JRNsuwWgXya%2BRPvCYP0hr3rsQecm8Oe8xpTN52yvmqnaoC8Gm%2Bq%2B6NqzznTihLJWOoJxttP2ZiRGByqN9WxyRyZS3VV274wK58NY6g%2B%2B7NadYbJ8b1WVYlRXpc0%2FKmSUzZ%2Fw67lm6ZL3fHAzMkO%2F%2BymyB1vDU43aMYd71wTHW0klJPKmNONvSorT07VrMjr5OmMeEgN7DMC2JA8KdKViAkcCqYgCYQkWh8INsrlQZckNJKYxirmoLXtZz4Mp0qrV6ZANOZ8cYodrJE3xdQ0tCkK472%2F4ITTRXebMPnkPVkoyFRSePJoM%2BKE4%2FUpnZOVK17RyfRnKAi8zZa5AJOnws9QoimaH6XCUCqZExoH%2FmKdmekM8xeGcu9%2F%2Biu4jbzVRvANki4qdfrgr7%2FqdXdonO9QZhAW9KjPxonJfGIAs%2BkBrJMDkEKZm1X5q5FUbSJ%2F9THj44dmeptKa22CEVnvvGJFRZ%2BSPe%2BpNShdOjhPlDJdKiiXul6IuiQfnRP6hYvpzwaIFapBTpQ6MMX7X%2BR53g9%2Fe2gbArcpBzc8tUtE9PoVxCJrllCI5Yfgdr0mYe3f8NzKAenFTO8Fir9ecj%2FwJv6veW4XGryWZNeqXXbbNext73Vvfjyl3JBC1VmXlNPzfEHaCplmTxGfFX6vyI7%2FetIvHD0B8g%2BXo%2B8wfApiTwqp0rsqzPeE1pHQOf1LZlzJ%2F%2BLmffaqj9NNlf9Fb84Bo8qBKojDij5VuJ6z2%2FGMUJLQD7PMCyO5uJagu0xVgWhAQTNeVjFJ3s6lrelAG7wD2V4KviyR%2BpIEQNFXwz83xn9160xMUcxXw9eREOVTxgRJl%2BNRr%2BxnK5qQU3Aiz4clv2VzCs4ny50M7Z2NIZ6M%2BmlCiFWMleq9gS41Uv4WTJKLn5DVEroaCHXEWKVIwpyDesLmni7UzUZETwQ5n4PXWop0Wqq0%2F5oinfgx%2FY1airn0h37Nyf8%3D)

@todo: Добавить на схему деприоритезацию/explicit best

## Quick Start
Сборка из аркадии:
```
$ cd arcadia/noc/dregress-checker
$ ya make
```
Создаём конфиг файл:
```
$ cat /etc/dregress-checker/dregress-checker.yaml 
logging:
  level: warn
  sinks:
    - stdout
  encoding: console

db_host: c-mdbiibt18lrbmle8koh8.rw.db.yandex.net
db_user: egress
db_password: {password}
solomon_token: {AQAD-token}
st_token: AQAD-ololo
```
{% note info %}

`c-mdbiibt18lrbmle8koh8.rw.db.yandex.net` - это тестовая база для дебага. Если нужно работать с продовой, то эту строчку нужно удалить.

{% endnote %}

{% note info %}

`st_token` - можно указать любое значение, если собираемся просто прогнать алгоритм для дебага.

{% endnote %}

Запускаем:
```
$ ./cmd/dregress-checker/dregress-checker --help
Usage of ./cmd/dregress-checker/dregress-checker:
  -c string
        config file (default "/etc/dregress-checker/dregress-checker.yaml")
  -d    debug mode
  -from string
        start time, example: 2022-05-16T07:36:00.000Z
  -s string
        set startrek ticket
  -to string
        end time, example: 2022-05-17T09:36:00.000Z
```
```
$ ./cmd/dregress-checker/dregress-checker -d -s TEST-1234 --from 2022-06-13T03:58:00.000Z --to 2022-06-13T04:19:00.000Z
...
From:  2022-06-13 06:58:00 +0300 MSK
To:  2022-06-13 07:19:00 +0300 MSK
...
DB ACTION:  4 TEST-1234 41202 neun@ae99.90 (Rostelecom2 500GE@M9 %cdn%) good 0 0 0 nothing
DB ACTION:  4 TEST-1234 41202 aurora@ae1.5 (ER-Telecom 40GE@SPBBM18 %peer%) unknown 0 20025 40000 nothing
DB ACTION:  4 TEST-1234 41202 dante@ae1.9 (Piter-IX 300GE@M9 %peer%) bad 0 54843 300000 deprior
...
```
{% note info %}

Время нужно указывать -3 часа.

{% endnote %}
## Прод сервера
Сейчас чекер работат на:
```
sas-egress.net.yandex.net
vla-egress.net.yandex.net
```
## Juggler
https://juggler.yandex-team.ru/raw_events/?query=service%3Ddregress-checker-loop
