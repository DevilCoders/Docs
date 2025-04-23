# Ограничения по странам Версия 1

## Методы

### getCountryRestrictions

#### Описание

```http request
GET /api/avia_country_restrictions/v1/data?toPointKey=c202 HTTP/1.1
Host: api.travel-balancer-test.yandex.net
X-Ya-Service-Ticket: <your_ticket_here>
X-Ya-UseCamelCase: true
```

### getExtendedCountryRestrictions

#### Описание

```http request
GET /api/avia_country_restrictions/v1/extended?toPointKey=c202 HTTP/1.1
Host: api.travel-balancer-test.yandex.net
X-Ya-Service-Ticket: <your_ticket_here>
X-Ya-UseCamelCase: true
```

## Требования к бэкенду

1. Бэкэнд на запрос с `toPointKey` (и опционально `fromPointKey`) отдает список ограничений в соответствии со [спецификацией](response.ts).
2. Если ничего нет, то 404.

## Требования к фронтенду

1. Фронтенд рендерит компоненты на выдаче.

## Метрики

Описание текущих метрик [здесь](https://wiki.yandex-team.ru/avia/dev/services-table/country-restrictions/#tekushhiemetriki)

## Получить `X-Ya-Service-Ticket`

1. В аркадии перейти по пути `/travel/hotels/tools/cli`
2. Выполнить `ya make`
3. Выполнить `./hotels-cli --cli-tvm-secret <secret_here> ticket`
4. Тикет появится в выводе терминала

`cli-tvm-secret` брать [отсюда](https://yav.yandex-team.ru/secret/sec-01dq7m5cccmhbgkeqt6pakj15k/)
