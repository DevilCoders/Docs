# Редиректы средствами any.yandex

1. Документация по созданию заявки есть на [wiki](https://wiki.yandex-team.ru/l7/any/).
2. Запрос [dns](https://dns.tt.yandex-team.ru/request). Обычно нужно делать A и AAAA (213.180.204.242 и 2a02:6b8::242).

Список наших доменов на any.yandex (список ведется вручную, т.к. простого инструмента понять какие домены туда попали нет, запросы хранятся в очереди https://st.yandex-team.ru/MINOTAUR/order:updated:true/filter):

HTTP

1. hotelyandex.ru
2. hotel-yandex.ru
3. hotels-yandex.ru
4. hotelsyandex.ru
5. yandex-hotels.ru
6. yandexhotel.ru
7. yandex-hotel.ru
8. busyandex.ru
9. bus-yandex.ru
10. yandex-bus.ru
11. yandexbus.ru

HTTPS

-   https://yandex.ru/travelyandex.ru/travel
-   https://m.travel.yandex.ru/
-   https://tourism.yandex.ru/
-   https://tours.yandex.ru/
-   https://travel.yandex/
-   https://travel.yandex.net/
-   https://turism.yandex.ru/
-   https://turizm.yandex.ru/
-   https://tury.yandex.ru/
-   https://yandex.travel/
-   https://mir.trains.yandex.ru/ -> https://travel.yandex.ru/trains

robots.txt

Запросы /robots.txt с доменов 3ds.travel.yandex.net, tourism.yandex.ru, travel-prod.yandex.ru, tours.yandex.ru, travel.yandex, travel.yandex.net, m.travel.yandex.ru, turism.yandex.ru, turizm.yandex.ru, tury.yandex.ru, yandex.travel переводятся на https://travel.yandex.ru/robots-disallow.txt
