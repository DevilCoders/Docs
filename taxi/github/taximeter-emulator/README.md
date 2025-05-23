# taximeter-emulator
Эмулятор водителей, работающих через таксометр.

## Управление заказами

Обработкой заказа можно управлять комментариями следующего вида:

```
param1 - value1, param2 - value2, ... ; db_id - db_id1, param1 - value1_1, ...; db_id - db_id2, param1 - value1_2, ...; ...
```

Комментарий разбивается на несколько групп параметров - общая группа и частные. Частная группа определяется параметром
db_id таксопарка и дополняет/переопределяет общие параметры, если заказ принял водитель этого парка.

### Параметры

- `seen_received - int`
    - время задержки отправки seen received водителя в секундах (по умолчанию = 0).
- `seen - int`
    - время реакции водителя в секундах (по умолчанию = 0).
- `reject - int`
    - отказ от заказа через указаное время в секундах.
- `speed - int`
    - скорость водителя в км/ч (по умолчанию = 40).
- `driving_speed - int`
    - скорость движения к клиенту в км/ч (по умолчанию = `speed`).
- `wait - int`
    - время ожидания клиента в секундах (по умолчанию = случайное число от 1 до 300).
- `transporting_speed - int`
    - скорость транспортировки клиента в км/ч (по умолчанию = `speed`).
- `status - <skip|cancelled> <assigned|driving|waiting|transporting>`
    - Если это возможно:
        - В случае `skip` `requestconfirm` с указанным статусом не будет отправлен.
        - В случае `cancelled` заказ на указанной стадии будет отменен водителем через `reject` секунд.
        - Статус `assigned ` можно только отменить (`canceled`; `skip` не валиден для него).
- `destination - longitude latitude`
    - точка вместо пункта назначения, в которой водитель завершит заказ.
    - пример: `destination - 37.6615 55.7373`
- `manual_control - 1`
    - переключает водителя, принявшего заказ, на ручное управление через ручку `/driver_control`.
- `accuracy - int`
    - значение accuracy, посылаемое в `gps/set` в течение заказа

## Дополнительные параметры
Эти параметры влияют на платеж в сервисе transactions.
Они дополнительно передаются к параметрам управления заказа в виде: 
```
param1, param2, ...
```
Эти комментарии достаточно один раз указать в общей группе параметров.

- `payment_holdfail`
    - делает платеж неуспешным с нетехнической ошибкой (not_enough_funds).
- `payment_holdfail_technical`
    - делает платеж неуспешным с технической ошибкой (tech_error).

## Окружение
Кондукторная группа: `%taxi_test_taximeter_emulator`

Проекты в TeamCity:
- [Тестинг](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Tools_TaximeterEmulator?mode=builds#all-projects)
- [PR](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Tools_TaximeterEmulatorPullRequest?mode=builds#all-projects)

Логи смотреть на хостах, `/var/log/yandex/taximeter-emulator/taxi.log`. В кибану не поставляются

## Включенные таксопарки

### Testing

Таксопарки разнесены на две машины `%taxi_test_taximeter_emulator`.

На `taximeter-emulator-myt-01.taxi.tst.yandex.net`

- Москва
    - 'Чирик', `db_id a3608f8f7ee84e0b9c21862beef7e48d`
- Краснодар
    - 'Красный Олимп', `db_id f918f022a23242e79f68cc95bd32692f`
- Берлин
    - 'Berlin bream', `db_id c5cdea22ad6b4e4da8f3fdbd4bddc2e7`

На `taximeter-emulator-vla-01.taxi.tst.yandex.net`

- Санкт-Петербург
    - 'Парадное такси', `db_id dc7b9c2d506c43e88d10944c92fcc5fe`
- Красноярск
    - 'Красное смещение', `db_id c55fe8b825304f0184d8f359c5d4ac8f`
- Тула
    - 'Самоездящий самовар', `db_id 4774f9571ef14ceeaae927debc51c633`
- Екатеринбург
    - 'Пышная Пышма', `db_id e1839f5e0d49454aa2a05b8952de552e`
- Нижний Новгород
    - 'Носорог', `db_id af06c802b2a844b39348ccdd78c1d230`
- Уфа
    - 'Утконос', `db_id 61f2b49faa2f4bb381cdbdf6073f7a30`
- Калининград
    - 'Калина', `db_id 07ed87032dcc426e8b1d41c2b256edaa`
- Сочи
    - 'Олимпийский Прикуп', `db_id 6b2d0a9ca29749dbbc05b0370aad1d9f`
- Омск
    - 'Лучше метро', `db_id 34210220db7744399083d24dd4d029bd`

## Ручки

Все эмуляторы слушают порт 8080.

- `POST /driver_control`

    Ручное управление водителем для интеграционных тестов.

- `POST /driver_positions`

    Принимает json.
    Меняет позиции водителей по одному из двух сценариев.

    Cписок полей:
    - `limit`
        - Максимум столько водителей будет обновлено; по умолчанию - 100.
    - `db_id`
        - Парк, водители которого будут обновлены.
        Обязательное поле, если `refresh` - `True`.
    - `refresh`
        - Если равняется `True`, то позиции водителей назначаются случайно.
    - `geopoint`
        - Если `refresh` не `True`, то ставит водителя в точку
        `(geopoint['longitude'], geopoint['latitude'])`.
    - `tariffs`
        - Список тарифов как они приходят с таксометра ('ЭКОНОМ' и пр.).
        Будут перемещены только те водители, которые могут принимать заказы
        указанных тарифов. Опционально.

    Возвращает:
    - `200` - если было перемещено `limit` водителей.
    - `203` - если `limit` не был достигнут.
    - `400` - если формат запроса невалидный.

## Локальный запуск эмулятора 

### Подготовка к запуску
1. [Подготовить окружение для разработки](https://wiki.yandex-team.ru/taxi/backend/howtostart/#podgotovkarazrabotcheskogookruzhenija)
2. Убедиться, что есть доступ до `http://core-driving-router.testing.maps.yandex.net`. Если нет, заказать через Puncher

### Запуск
Осуществляется запуском скрипта run_one_driver.py (или run_local.sh - в нём заданы все необходимые аргументы для run_one_driver.py). После его запуска можно в приложении Такси произвести заказ такси у эмулируемого водителя.
Запуск скрипта осуществляется следующим образом.

`python3.7 run_one_driver.py --phone PHONE --env ENV [--db_id DB_ID][--starting_point LONGITUDE LATITUDE][--city CITY]`

Cписок аргументов:
- `phone`
    - Номер телефона водителя парка. Обязательное поле. Можно выбрать любого водителя в оффлайне из парков, работающих с эмулятором.
- `env`
    - Выбор окружения, в котором будет запускаться эмулятор. Доступные опции: `unstable`, `testing`
- `db_id`
    - ID парка, водитель которого будет запущен. Параметр нужно указать в случае, когда введенному номеру телефона 
соответствует несколько парков. Если же номеру телефона соответствует только один парк, то этот параметр вводить 
необязательно.
- `starting_point`
    - Начальная координата водителя. Если этот парамерт указан, то нужно ввести два числа с 
плавающей точкой в качестве начальной координаты. Если параметр не указан, то в качестве начальной точки
выбирается стандартное местоположение. Если его нет, то точка выбирается случайно. Стандартные местоположения есть 
лишь для городов Москва и Санкт-Петербург, и расположены они рядом с офисом Яндекса (для Москвы - возле Авроры).

- `city`
    - Город, в котором находится водитель. По умолчанию: `moscow`. Доступные города: `moscow`, `krasnoyarsk`,
`saint_petersburg`, `tula`, `ekaterinburg`, `nizhniy_novgorod`, `ufa`, `kaliningrad`, `sochi`, `omsk`, 
`krasnodar`, `gelenzhik`, `kislovodsk`, `chelyabinsk`, `makhachkala`, `izhevsk`, `volgograd`, `berlin`, `bishkek`, `tel_aviv`.
