---
title: Локальный запуск процесса продажи
rank: 30
---

Гайд, как запустить локально Travel API + Orchestrator - чтобы работал основной флоу покупки билета на поезд через generic order.

### Подготовка инфраструктуры
1. Добиться, чтобы оркестратор и апи запускались локально - по [гайду](https://docs.yandex-team.ru/travel/services/orders/start)
   Нужно иметь локальные конфигурационные файлы для них, например:
   ```
   /Users/monitorius/work/arc/arcadia/travel/orders/app/src/main/resources/application-local.yml
   /Users/monitorius/work/arc/arcadia/travel/api/src/main/resources/application-local.yml
   ```
   И, соотвественно, профили dev и local должны быть прописан в IDEA в active profiles. Они будут применяться поверх настроек application.yml приложения.

{% cut "картинка" %}

![idea profiles](https://jing.yandex-team.ru/files/monitorius/2020-12-24_14-29-38.png)

{% endcut %}

АПИ и Орк запускают /actuator на порту 8080, соотвественно с дефолтным конфигом одновременно не могут запуститься. Нужно изменить настройку в любого из них, чтобы порты не конфликтовали
```
management:
    server:
        port: 8081
```

2. Поставить локальный postgres.
   Для macos+brew приблизительно так:
   ```
   brew install postgresql@12  # нужная нам версия базы. Ставится, но даже клиент psql сходу не заведется
   brew install postgresql     # поставит 13+ версию, но зато и пропишет в PATH бинарники pg, чтобы работал psql и другие команды pg
   brew services start postgresql@12  # если не заводится, смотрим в лог /usr/local/var/log.postgresql@12.log
   createdb $USER
   createdb orders
   ```
   Для ubuntu:
   ```
   sudo apt-get install postgresql
   sudo -u postgres psql  # Заходим в бд под пользователем postgresql
   postgresql=# alter user postgres password 'postgres';  # Устанавливаем пароль
   postgresql=# \q  # Выходим
   sudo nano /etc/postgresql/12/main/pg_hba.conf  # В файле надо поменять METHOD на md5 или trust, чтобы входить с паролем
   sudo service postgresql restart
   ```
   
3. Готовимся к миграциям базы
   ```
   psql # заходим в консоль pg
   \c orders
   CREATE EXTENSION pg_trgm;
   CREATE EXTENSION "uuid-ossp";
   ```

### Настройка Оркестратора
При запуске с таким конфигом Орк при старте применит все нужные миграции в pg к базе orders.
```
server:
    port: 8080
management:
    server:
        port: 8080
# ходим в локальный postgres        
spring:
    jpa:
        hibernate:
            ddl-auto: validate
            jdbc:
                batch_size: 50
        properties:
            hibernate:
                dialect: ru.yandex.travel.hibernate.dialects.CustomPostgresqlDialect
                jdbc:
                    time_zone: UTC
        show-sql: false
    datasource:
        url: jdbc:postgresql://localhost:5432/orders
        username: monitorius
        password: ''
trust-train:
    service-token:  # из yav https://yav.yandex-team.ru/secret/sec-01d6wpth9ytbyqg9vk3kbtea3r/explore/versions
trust-db-mock:
    enabled: true

# конфиг тестинга Инновационной Мобильности        
im:
    base-url: https://testing.ipv4-proxy.internal.rasp.yandex.net/im-test/
    http-read-timeout: 180000
    http-request-timeout: 180000
    pos:       # из yav https://yav.yandex-team.ru/secret/sec-01dznp44a7qvrhd04yevxj5gkv/explore/versions
    login:     # из yav
    password:  # из yav
    test-cases.enabled: true

# скачать общие справочники на винт и прописать в конфиг.
# справочники берем из ресурсов последней задачи https://sandbox.yandex-team.ru/tasks?    
train-dictionaries:
    enabled: true
    tariff-info.data-file: /Users/monitorius/work/data/travel/dicts/train_tariffinfo.data

train-workflow:
    rebooking-enabled: true
    order-expiration-time: 20m
    promo-hotel-2020.enabled: true
```
### Настройка Travel API
```
server:
    port: 8090

# не конфликтуем с орком за порт /actuator
management:
    server:
        port: 8081

# локальный порт grpc орка
orchestrator:
    mode: TARGETS
    targets: localhost:30858

# скачать общие справочники на винт и прописать в конфиг.
# справочники берем из ресурсов последней задачи https://sandbox.yandex-team.ru/tasks?children=true&hidden=false&type=DUMP_RASP_DATA
train-dictionaries:
    enabled: true
    country.data-file: /Users/monitorius/work/data/travel/dicts/country.data
    country.capacity-coefficient: 25.0
    station.data-file: /Users/monitorius/work/data/travel/dicts/station.data
    station.capacity-coefficient: 3.0
    station-code.data-file: /Users/monitorius/work/data/travel/dicts/station_code.data
    station-code.capacity-coefficient: 2.0
    readable-timezone.data-file: /Users/monitorius/work/data/travel/dicts/readable_timezone.data
    readable-timezone.capacity-coefficient: 20.0
    settlement.data-file: /Users/monitorius/work/data/travel/dicts/settlement.data
    settlement.capacity-coefficient: 3.0
    tariff-info.data-file: /Users/monitorius/work/data/travel/dicts/train_tariffinfo.data
    tariff-info.capacity-coefficient: 20.0
    timezone.data-file: /Users/monitorius/work/data/travel/dicts/timezone.data
    timezone.capacity-coefficient: 10.0
    station-express-alias.data-file: /Users/monitorius/work/data/travel/dicts/station_express_alias.data
    station-express-alias.capacity-coefficient: 10.0

train-offer:
  mode: YP
  yp:
    endpoint-set-id: trains-offer-storage-testing.main.grpc
tvm:
    enabled: false
    client-id: 1200
    client-secret: 1200

# конфиг тестинга Инновационной Мобильности
im:
    base-url: https://testing.ipv4-proxy.internal.rasp.yandex.net/im-test/
    http-read-timeout: 180000
    http-request-timeout: 180000
    pos:       # из yav https://yav.yandex-team.ru/secret/sec-01dznp44a7qvrhd04yevxj5gkv/explore/versions
    login:     # из yav
    password:  # из yav
    test-cases.enabled: true
```

При локальной покупке могут возникать исключения вида `No such country for geoId: 225`
Для решения необходимо добавить в конфиг:
```
train-country:
  enabled: true
  proxy: hahn.yt.yandex.net
  table-path: //home/travel/testing/rasp_dicts/latest/country
  index-path: /home/maxim-sazonov/IdeaProjects/data/train_country_index  # Нужно указать любой путь в доступной папке (в данном случае data), папка с индексом создастся сама
train-station-code:
  enabled: true
  proxy: hahn.yt.yandex.net
  table-path: //home/travel/testing/rasp_dicts/latest/station_code
  index-path: /home/maxim-sazonov/IdeaProjects/data/train_station_index  # Нужно указать любой путь в доступной папке (в данном случае data), папка с индексом создастся сама
```
По умолчанию эти провайдеры выключены, т.к. они не требуются многим клиентам оркестратора (отели, авиа, тесты)

### Дырки
- до ipv4-proxy, чтобы ходить в ИМ
  testing.ipv4-proxy.internal.rasp.yandex.net:443
- до тестовой Офферницы
  train-offer-storage-test.stable.qloud-b.yandex.net:9111

{% cut "зачем" %}

```
@ganintsev
в апи собирается payload услуги из данных оффера и персональных, потом эта инфа отправляется в орк на создание заказа
такчто создать заказ без офферницы сейчас не получится
только если без апи, но это сложно
```

{% endcut %}

### Запуск workflow покупки жд-билета
Есть классный скрипт имени @ganintsev, прогоняющий флоу покупки так, как это примерно делает фронтенд, ходящий в Travel API: [generic_client](https://a.yandex-team.ru/arc_vcs/travel/orders/tools/generic_client/__main__.py?rev=622f3c1a30f197476cfa16863051ed6632f1cc24)


Если у вас запущены локально апи и орк, то делаем примерно так:
```
cd /Users/monitorius/work/arc/arcadia/travel/orders/tools/generic_client
ya make
Y_PYTHON_SOURCE_ROOT="/Users/monitorius/work/arc/arcadia" ./generic_client --skip-authentication --mock-payment
```

{% cut "Выдача скрипта будет примерно такой" %}

```
2020-12-24 15:01:36,514 | INFO | http://train-offer-storage-test.stable.qloud-b.yandex.net:80/store => 200
2020-12-24 15:01:36,515 | INFO | {"offer_id":"7f7dbd16-0ff1-475c-87ef-bd3e2681a650","label_hash":"suT-_32jrS09c90T9ZIFsFRZL9K69W2XGVVNCqg"}

2020-12-24 15:01:36,625 | INFO | http://localhost:8090/api/generic_booking_flow/v1/create_order => 200
2020-12-24 15:01:36,626 | INFO | {"id":"1e06c071-f093-4a26-a022-4a987a543c85","pretty_id":"YA-0000-0006-5536","state":null,"display_state":"OS_IN_PROGRESS","expires_at":null,"serviced_at":"2021-02-09T02:45:00Z","services":[{"id":"4125d783-6290-47fd-b466-44e3cab26fef","service_type":"TRAIN","hotel_info":null,"train_info":{"error":null,"insurance_status":null,"partner_order_id":0,"reservation_number":null,"station_from":{"id":2006004,"title":"Москва (Ленинградский вокзал)","popular_title":"Ленинградский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":213,"settlement_geo_id":213,"settlement_title":"Москва"},"station_to":{"id":9602494,"title":"Санкт-Петербург (Московский вокзал)","popular_title":"Московский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":2,"settlement_geo_id":2,"settlement_title":"Санкт-Петербург"},"train_info":{"train_title":"Москва — Санкт-Петербург","start_station_title":"","end_station_title":"","start_settlement_title":"Москва ","end_settlement_title":"Санкт-Петербург","brand_title":"САПСАН","train_ticket_number":"752А","train_number":"752А","suburban":false},"car_type":null,"compartment_gender":null,"arrival":null,"departure":"2021-02-09T02:45:00Z","partner":"im","car_number":null,"special_notice":null,"warnings":null,"two_storey":false,"coach_owner":null,"passengers":[{"tickets":[],"doc_id":"6500112233","doc_type":"ПН","citizenship":"RU","first_name":"Илья","last_name":"Сугробин","patronymic":"Викторович","age":31,"birth_date":"1990-01-01","sex":"M","customer_id":null,"insurance":null,"is_non_refundable_tariff":false}],"only_full_return_possible":false,"full_refund_possible":true,"rebooking_available":false}}],"order_price_info":{"price":{"value":0,"currency":"RUB"},"original_price":{"value":0,"currency":"RUB"},"discount_amount":{"value":0,"currency":"RUB"},"promo_campaigns":null,"promo_code_application_results":null},"payment":null,"contact_info":{"email":"user@example.org","phone":"+71234567890"}}
2020-12-24 15:01:36,626 | INFO | Создали заказ 1e06c071-f093-4a26-a022-4a987a543c85
2020-12-24 15:01:36,650 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:36,650 | INFO | {"state":"NEW","version_hash":""}
2020-12-24 15:01:37,665 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:37,665 | INFO | {"state":"WAITING_RESERVATION","version_hash":"1898073962"}
2020-12-24 15:01:38,681 | INFO | ^^^ Same response ^^^
2020-12-24 15:01:39,691 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:39,691 | INFO | {"state":"RESERVED","version_hash":"262950650"}
2020-12-24 15:01:40,739 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_info?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:40,739 | INFO | {"id":"1e06c071-f093-4a26-a022-4a987a543c85","pretty_id":"YA-0000-0006-5536","state":"RESERVED","display_state":"OS_AWAITS_PAYMENT","expires_at":"2020-12-24T10:16:36.586695Z","serviced_at":"2021-02-09T02:45:00Z","services":[{"id":"4125d783-6290-47fd-b466-44e3cab26fef","service_type":"TRAIN","hotel_info":null,"train_info":{"error":null,"insurance_status":"PRICED","partner_order_id":2848520,"reservation_number":"71010939468762","station_from":{"id":2006004,"title":"Москва (Ленинградский вокзал)","popular_title":"Ленинградский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":213,"settlement_geo_id":213,"settlement_title":"Москва"},"station_to":{"id":9602494,"title":"Санкт-Петербург (Московский вокзал)","popular_title":"Московский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":2,"settlement_geo_id":2,"settlement_title":"Санкт-Петербург"},"train_info":{"train_title":"Москва — Санкт-Петербург","start_station_title":"","end_station_title":"","start_settlement_title":"Москва ","end_settlement_title":"Санкт-Петербург","brand_title":"САПСАН","train_ticket_number":"752А","train_number":"752А","suburban":false},"car_type":"sitting","compartment_gender":null,"arrival":"2021-02-09T06:15:00Z","departure":"2021-02-09T02:45:00Z","partner":"im","car_number":"04","special_notice":null,"warnings":[],"two_storey":false,"coach_owner":"ДОСС РЖД","passengers":[{"tickets":[{"places":[{"number":"004","type":null,"type_text":null}],"tariff_info":null,"rzhd_status":null,"amount":{"value":2218.224,"currency":"RUB"},"raw_tariff_title":"Полный","booked_tariff_code":"full","payment":{"amount":{"value":1998.4,"currency":"RUB"},"fee":{"value":219.824,"currency":"RUB"},"bedding_amount":{"value":0,"currency":"RUB"}},"blank_id":2306949,"can_change_electronic_registration_till":null,"can_return_till":null,"pending":false,"refundable":false,"discount_denied":false}],"doc_id":"6500112233","doc_type":"ПН","citizenship":"RU","first_name":"Илья","last_name":"Сугробин","patronymic":"Викторович","age":31,"birth_date":"1990-01-01","sex":"M","customer_id":4583840,"insurance":{"compensation":{"value":350000,"currency":"RUB"},"amount":{"value":100,"currency":"RUB"}},"is_non_refundable_tariff":false}],"only_full_return_possible":false,"full_refund_possible":true,"rebooking_available":false}}],"order_price_info":{"price":{"value":2218.22,"currency":"RUB"},"original_price":{"value":2218.22,"currency":"RUB"},"discount_amount":{"value":0,"currency":"RUB"},"promo_campaigns":{"taxi2020":{"eligible":false},"mir2020":{"eligible":false,"cashback_amount":null,"cashback_amount_string":null}},"promo_code_application_results":null},"payment":null,"contact_info":{"email":"user@example.org","phone":"+71234567890"}}
2020-12-24 15:01:40,777 | INFO | http://localhost:8090/api/generic_booking_flow/v1/add_service => 200
2020-12-24 15:01:40,777 | INFO | {"service_id":"cb5d6aeb-e282-40bf-a69b-9dd6853d78c7"}
2020-12-24 15:01:40,787 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:40,787 | INFO | {"state":"RESERVED","version_hash":"262950650"}
2020-12-24 15:01:41,801 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:41,801 | INFO | {"state":"WAITING_RESERVATION","version_hash":"1225052702"}
2020-12-24 15:01:42,816 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:42,817 | INFO | {"state":"RESERVED","version_hash":"-410070610"}
2020-12-24 15:01:43,819 | INFO | Добавили страховку
2020-12-24 15:01:43,871 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_info?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:43,872 | INFO | {"id":"1e06c071-f093-4a26-a022-4a987a543c85","pretty_id":"YA-0000-0006-5536","state":"RESERVED","display_state":"OS_AWAITS_PAYMENT","expires_at":"2020-12-24T10:16:36.586695Z","serviced_at":"2021-02-09T02:45:00Z","services":[{"id":"4125d783-6290-47fd-b466-44e3cab26fef","service_type":"TRAIN","hotel_info":null,"train_info":{"error":null,"insurance_status":"PRICED","partner_order_id":2848520,"reservation_number":"71010939468762","station_from":{"id":2006004,"title":"Москва (Ленинградский вокзал)","popular_title":"Ленинградский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":213,"settlement_geo_id":213,"settlement_title":"Москва"},"station_to":{"id":9602494,"title":"Санкт-Петербург (Московский вокзал)","popular_title":"Московский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":2,"settlement_geo_id":2,"settlement_title":"Санкт-Петербург"},"train_info":{"train_title":"Москва — Санкт-Петербург","start_station_title":"","end_station_title":"","start_settlement_title":"Москва ","end_settlement_title":"Санкт-Петербург","brand_title":"САПСАН","train_ticket_number":"752А","train_number":"752А","suburban":false},"car_type":"sitting","compartment_gender":null,"arrival":"2021-02-09T06:15:00Z","departure":"2021-02-09T02:45:00Z","partner":"im","car_number":"04","special_notice":null,"warnings":[],"two_storey":false,"coach_owner":"ДОСС РЖД","passengers":[{"tickets":[{"places":[{"number":"004","type":null,"type_text":null}],"tariff_info":null,"rzhd_status":null,"amount":{"value":2218.224,"currency":"RUB"},"raw_tariff_title":"Полный","booked_tariff_code":"full","payment":{"amount":{"value":1998.4,"currency":"RUB"},"fee":{"value":219.824,"currency":"RUB"},"bedding_amount":{"value":0,"currency":"RUB"}},"blank_id":2306949,"can_change_electronic_registration_till":null,"can_return_till":null,"pending":false,"refundable":false,"discount_denied":false}],"doc_id":"6500112233","doc_type":"ПН","citizenship":"RU","first_name":"Илья","last_name":"Сугробин","patronymic":"Викторович","age":31,"birth_date":"1990-01-01","sex":"M","customer_id":4583840,"insurance":{"compensation":{"value":350000,"currency":"RUB"},"amount":{"value":100,"currency":"RUB"}},"is_non_refundable_tariff":false}],"only_full_return_possible":false,"full_refund_possible":true,"rebooking_available":false}},{"id":"cb5d6aeb-e282-40bf-a69b-9dd6853d78c7","service_type":"TRAIN_INSURANCE","hotel_info":null,"train_info":null}],"order_price_info":{"price":{"value":2318.22,"currency":"RUB"},"original_price":{"value":2318.22,"currency":"RUB"},"discount_amount":{"value":0,"currency":"RUB"},"promo_campaigns":{"taxi2020":{"eligible":false},"mir2020":{"eligible":false,"cashback_amount":null,"cashback_amount_string":null}},"promo_code_application_results":null},"payment":null,"contact_info":{"email":"user@example.org","phone":"+71234567890"}}
2020-12-24 15:01:44,933 | INFO | http://localhost:8090/api/generic_booking_flow/v1/start_payment => 200
2020-12-24 15:01:44,933 | INFO |
2020-12-24 15:01:44,934 | INFO | Запустили оплату
2020-12-24 15:01:44,944 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:44,944 | INFO | {"state":"STARTING_PAYMENT","version_hash":"-410070610"}
2020-12-24 15:01:45,959 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:45,959 | INFO | {"state":"WAITING_PAYMENT","version_hash":"-410070610"}
2020-12-24 15:01:46,960 | INFO | Заказ ожидает оплаты 1e06c071-f093-4a26-a022-4a987a543c85
2020-12-24 15:01:46,997 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_info?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:46,998 | INFO | {"id":"1e06c071-f093-4a26-a022-4a987a543c85","pretty_id":"YA-0000-0006-5536","state":"WAITING_CONFIRMATION","display_state":"OS_IN_PROGRESS","expires_at":"2020-12-24T10:16:36.586695Z","serviced_at":"2021-02-09T02:45:00Z","services":[{"id":"4125d783-6290-47fd-b466-44e3cab26fef","service_type":"TRAIN","hotel_info":null,"train_info":{"error":null,"insurance_status":"PRICED","partner_order_id":2848520,"reservation_number":"71010939468762","station_from":{"id":2006004,"title":"Москва (Ленинградский вокзал)","popular_title":"Ленинградский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":213,"settlement_geo_id":213,"settlement_title":"Москва"},"station_to":{"id":9602494,"title":"Санкт-Петербург (Московский вокзал)","popular_title":"Московский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":2,"settlement_geo_id":2,"settlement_title":"Санкт-Петербург"},"train_info":{"train_title":"Москва — Санкт-Петербург","start_station_title":"","end_station_title":"","start_settlement_title":"Москва ","end_settlement_title":"Санкт-Петербург","brand_title":"САПСАН","train_ticket_number":"752А","train_number":"752А","suburban":false},"car_type":"sitting","compartment_gender":null,"arrival":"2021-02-09T06:15:00Z","departure":"2021-02-09T02:45:00Z","partner":"im","car_number":"04","special_notice":null,"warnings":[],"two_storey":false,"coach_owner":"ДОСС РЖД","passengers":[{"tickets":[{"places":[{"number":"004","type":null,"type_text":null}],"tariff_info":null,"rzhd_status":null,"amount":{"value":2218.224,"currency":"RUB"},"raw_tariff_title":"Полный","booked_tariff_code":"full","payment":{"amount":{"value":1998.4,"currency":"RUB"},"fee":{"value":219.824,"currency":"RUB"},"bedding_amount":{"value":0,"currency":"RUB"}},"blank_id":2306949,"can_change_electronic_registration_till":null,"can_return_till":null,"pending":false,"refundable":false,"discount_denied":false}],"doc_id":"6500112233","doc_type":"ПН","citizenship":"RU","first_name":"Илья","last_name":"Сугробин","patronymic":"Викторович","age":31,"birth_date":"1990-01-01","sex":"M","customer_id":4583840,"insurance":{"compensation":{"value":350000,"currency":"RUB"},"amount":{"value":100,"currency":"RUB"}},"is_non_refundable_tariff":false}],"only_full_return_possible":false,"full_refund_possible":true,"rebooking_available":false}},{"id":"cb5d6aeb-e282-40bf-a69b-9dd6853d78c7","service_type":"TRAIN_INSURANCE","hotel_info":null,"train_info":null}],"order_price_info":{"price":{"value":2318.22,"currency":"RUB"},"original_price":{"value":2318.22,"currency":"RUB"},"discount_amount":{"value":0,"currency":"RUB"},"promo_campaigns":{"taxi2020":{"eligible":false},"mir2020":{"eligible":false,"cashback_amount":null,"cashback_amount_string":null}},"promo_code_application_results":null},"payment":{"current":{"payment_url":"","amount":null,"type":null},"next":null,"error":{"code":"OTHER","amount":null},"receipts":[{"url":"http://fiscal.receipt/d484a6a5-041d-4688-b925-825ef9fa0a56","type":"FRT_ACQUIRE"}],"may_be_started":false,"uses_deferred_payments":false,"amount_paid":null,"payment_url":"","error_info":"OTHER"},"contact_info":{"email":"user@example.org","phone":"+71234567890"}}
2020-12-24 15:01:47,009 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:47,009 | INFO | {"state":"WAITING_CONFIRMATION","version_hash":"-1277299544"}
2020-12-24 15:01:49,023 | INFO | ^^^ Same response ^^^
2020-12-24 15:01:51,033 | INFO | ^^^ Same response ^^^
2020-12-24 15:01:53,045 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_state?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:53,045 | INFO | {"state":"CONFIRMED","version_hash":"-1829747320"}
2020-12-24 15:01:55,047 | INFO | Билеты выкуплены
2020-12-24 15:01:55,047 | INFO | Счастливого пути!
2020-12-24 15:01:55,436 | INFO | http://localhost:8090/api/generic_booking_flow/v1/get_order_info?orderId=1e06c071-f093-4a26-a022-4a987a543c85 => 200
2020-12-24 15:01:55,436 | INFO | {"id":"1e06c071-f093-4a26-a022-4a987a543c85","pretty_id":"YA-0000-0006-5536","state":"CONFIRMED","display_state":"OS_FULFILLED","expires_at":"2020-12-24T10:16:36.586695Z","serviced_at":"2021-02-09T02:45:00Z","services":[{"id":"4125d783-6290-47fd-b466-44e3cab26fef","service_type":"TRAIN","hotel_info":null,"train_info":{"error":null,"insurance_status":"PRICED","partner_order_id":2848520,"reservation_number":"71010939468762","station_from":{"id":2006004,"title":"Москва (Ленинградский вокзал)","popular_title":"Ленинградский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":213,"settlement_geo_id":213,"settlement_title":"Москва"},"station_to":{"id":9602494,"title":"Санкт-Петербург (Московский вокзал)","popular_title":"Московский вокзал","timezone":"Europe/Moscow","railway_timezone":"Europe/Moscow","settlement_id":2,"settlement_geo_id":2,"settlement_title":"Санкт-Петербург"},"train_info":{"train_title":"Москва — Санкт-Петербург","start_station_title":"","end_station_title":"","start_settlement_title":"Москва ","end_settlement_title":"Санкт-Петербург","brand_title":"САПСАН","train_ticket_number":"752А","train_number":"752А","suburban":false},"car_type":"sitting","compartment_gender":null,"arrival":"2021-02-09T06:15:00Z","departure":"2021-02-09T02:45:00Z","partner":"im","car_number":"04","special_notice":null,"warnings":[],"two_storey":false,"coach_owner":"ДОСС РЖД","passengers":[{"tickets":[{"places":[{"number":"004","type":null,"type_text":null}],"tariff_info":null,"rzhd_status":"REMOTE_CHECK_IN","amount":{"value":2218.224,"currency":"RUB"},"raw_tariff_title":"Полный","booked_tariff_code":"full","payment":{"amount":{"value":1998.4,"currency":"RUB"},"fee":{"value":219.824,"currency":"RUB"},"bedding_amount":{"value":0,"currency":"RUB"}},"blank_id":2306949,"can_change_electronic_registration_till":"2021-02-09T01:45:00Z","can_return_till":"2021-02-09T01:45:00Z","pending":false,"refundable":false,"discount_denied":false}],"doc_id":"6500112233","doc_type":"ПН","citizenship":"RU","first_name":"Илья","last_name":"Сугробин","patronymic":"Викторович","age":31,"birth_date":"1990-01-01","sex":"M","customer_id":4583840,"insurance":{"compensation":{"value":350000,"currency":"RUB"},"amount":{"value":100,"currency":"RUB"}},"is_non_refundable_tariff":false}],"only_full_return_possible":false,"full_refund_possible":true,"rebooking_available":false}},{"id":"cb5d6aeb-e282-40bf-a69b-9dd6853d78c7","service_type":"TRAIN_INSURANCE","hotel_info":null,"train_info":null}],"order_price_info":{"price":{"value":2318.22,"currency":"RUB"},"original_price":{"value":2318.22,"currency":"RUB"},"discount_amount":{"value":0,"currency":"RUB"},"promo_campaigns":{"taxi2020":{"eligible":false},"mir2020":{"eligible":false,"cashback_amount":null,"cashback_amount_string":null}},"promo_code_application_results":null},"payment":{"current":{"payment_url":"","amount":null,"type":null},"next":null,"error":{"code":"OTHER","amount":null},"receipts":[{"url":"http://fiscal.receipt/d484a6a5-041d-4688-b925-825ef9fa0a56","type":"FRT_ACQUIRE"}],"may_be_started":false,"uses_deferred_payments":false,"amount_paid":null,"payment_url":"","error_info":"OTHER"},"contact_info":{"email":"user@example.org","phone":"+71234567890"}}
```

{% endcut %}

Всё, покупка работает. Можно играться с дебаггером, смотреть в локальную базу и т.д.
Получить order info можно например так:
```
curl -H "X-Ya-YandexUid: 32431324" -H "X-Ya-Session-Key: 2412412341" "http://localhost:8090/api/generic_booking_flow/v1/get_order_info?orderId=a482efad-5f46-4129-937f-8229fc946689"
```
(YandexUid и Session-Key захардкожены в скрипте. Их можно передать в скрипт как параметры )

### Возможные проблемы
{% cut "В логах апи ошибка java.nio.file.NoSuchFileException: /cache/yp-discovery-train-offer.json" %}

Возникает, если нет доступа к `/cache`. Для решения указать в конфиге:
```
train-offer:
  yp:
    local-cache-path: /tmp/yp-discovery-train-offer.json  # Любой путь до файла с правами на запись
```

{% endcut %}

{% cut "В логах апи ошибка ru.yandex.travel.orders.client.HAGrpcException: No ready channels present" %}

Возникает, если нет доступа к оффернице.
Проверить можно [тут](https://puncher.yandex-team.ru/?destination=_RASP_TEST_NETS_&rules=exclude_inactive&sort=destination), добавив в Источники своего пользователя.
Должно выглядеть примерно так:
![puncher rules](https://jing.yandex-team.ru/files/maxim-sazonov/Screenshot%20from%202021-10-13%2016-53-03.png)
Также можно попробовать прописать в конфиге:
```
train-offer:
  mode: TARGETS
  targets: offer-storage.k24xgvdzx5zuss56.sas.yp-c.yandex.net
```
Проверить наличие доступа также можно с помощью запроса:
```
grpcurl -plaintext -H "X-Ya-Service-Ticket:$SERVICE_TICKET" -d '{"OfferId": "86579549-43f5-4f48-8e47-433980a85f6e"}' offer-storage.k24xgvdzx5zuss56.sas.yp-c.yandex.net:9111 NTrain.NOfferStorageApi.OfferStorageApiServiceV1/GetOffer
```
`grpcurl` нужно скачать [отсюда](https://github.com/fullstorydev/grpcurl/releases)

{% endcut %}

{% cut "Множественные exception-ы в логах орка" %}

Это нормально, если не мешает работе. Локально не все доступно и не все нужно

{% endcut %}

