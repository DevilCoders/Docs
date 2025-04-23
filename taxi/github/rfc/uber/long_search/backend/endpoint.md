# Endpoint для cost + eta в go

Endpoint для получения cost + eta + deeplink для Go

## Когда предполагается вызов
На клиенте uber, когда пользователь хочет отменить заказ(через 10-15 секунд,время регулируется [тут](#exp-time-new-flow)) отмена "как обычно" - позже экран отмены/редиректа в Go, при наличии установленного Go)

## API
Ручка: `4.0/mlutp/v1/taxi_order_deeplink`  
Request:
```json
{
  "route": [
    [55.1, 35],
    [56, 32.3]
  ],
  "selected_class": "uberx"
}
```
Response:
```json
{
  "description": "~180 $SIGN, ~2 мин$",
  "deeplink": "yandextaxi://...",
  "currency_rules": {
    "code": "RUB",
    "sign": "₽",
    "template": "$VALUE$ $SIGN$$CURRENCY$",
    "text": "руб."
  },
}
```
Legend:  
`route` - точки маршрута, заданные пользователем `[lon, lat]`(Первая - точка старта, последняя - точка конца)  
`selected_class` - класс тарифа(в терминах Uber)  
`description` - строка примерных cost + ETA([почему цена примерная](#Почему-цена-примерная))  
`deeplink` - deeplink для запуска Go с нужными параметрами. Ссылка не универсальная, в отсутствии Go работать не будет. Используются только первая и последняя точки маршрута

## Если ручка не работает
Не показывать редирект в Go

## Details
Предполагается собирать deeplink ручкой из входных данных и тарифа  
ETA + cost получать из `pricing` `v2/prepare`([схема](https://github.yandex-team.ru/taxi/schemas/blob/develop/schemas/services/pricing-data-preparer/api/v2_prepare.yaml))  
Для pricing нужен zone и Go-tariff. Zone можно получить из `superapp-misc` `v1/nearest_zone`([дока](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/superapp-misc/api/nearest_zone/#40mlutpv1nearest_zone))  
Для получения тарифа предлагаю завести taxi-config вида
```json
"TARIFFS_TRANSLATIONS_UBER_TO_GO": {
  "uberx": "econom",
  "uberselect": "comfort"
}
```
Тарифы Uber перечислены в [конфиге](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/UBER_CATEGORIES)  
Т.к. `v1/widgets` похоже реализует почти тот же функционал вероятно лучше всего выделить ручку в сервисе которая будет выполнять общую работу для `v1/widgets` и новой ручки

## Notes
* [структура deeplink](https://wiki.yandex-team.ru/taxi/mobile/externalrun/)
* Диплинки для yandextaxi и yandexyango отличаются. Сейчас планируется только yandextaxi

## Почему цена примерная
Сложно по offer_id восстановить весь саммари, не возвращая все данные из routestats

## Exp time new flow
Клиентсикй эксперимент 3.0 из `totw` 
Регулирует время, через которое должен работать новый экран отмены
```json
"uber_long_search_cancel_new_flow": {
  "time_sec": 15
}
```
`time` - время(в секундах) с начала заказа, после которого нужен новый флоу отмены