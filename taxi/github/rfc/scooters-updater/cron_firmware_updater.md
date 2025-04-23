
**Какую задачу решаем?**

Нам необходимо сделать крону обновления прошивок самокатов.
Крона должна быть управляема через конфиг + эксперимент.

Через конфиг будем настраивать основные параметры процесса.
Через эксперименты будем фильтровать самокаты и определять, нужно ли обновление для самоката.

Сейчас для обновления прошивок используется скрипт:
https://a.yandex-team.ru/arcadia/taxi/infra/tools-py3/taxi_scooters-misc/update_firmware.py

Из него надо будет брать логику обновления.

**Конфиг**

```
{
   'enable': true, // Здесь мы сразу можем включать/отключать все обновления
   'interval': 30, // Период запуска Periodic процесса (минуты или секунды, надо еще проверить)
   'firmware_types': [ // Типы прошивок, которые мы можем обновлять
      'iot': {
         'updating_enabled': true,  // Обновляем или нет
         'stq_max_count': '100', // Кол-во stq, которое может выполняться одновременно для данного типа прошивок
      },
      'ecu': {
         'updating_enabled': true,  // Обновляем или нет
         'stq_max_count': '100', // Кол-во stq, которое может выполняться одновременно для данного типа прошивок
      },
      ...
   ],
   'stq_retries': 3, // кол-во попыток обновить прошивку в stq,
   'stq_max_count': 10000, // кол-во stq, которое максимально может быть в очереди для всех прошивок
}
```
firmware_types:
1. iot
2. ecu
3. ble
4. gps
5. audio_lock
6. audio_unlock
7. audio_battery_low
8. audio_full
9. cable_lock

**Эксперимент**

В эксперимент будет передаваться json с информацией о самокате и типом запрашиваемой прошивки.
Результатом будет информация о том, есть ли обновление для самоката (тип обновления и ссылка на прошивку) или нет.

Пример json, который будет уходить в эксперимент:
```
{
   'type': 'iot', // firmware_types, тип прошивки, которую хотим обновить
   'scooter_num': '3412', // номер самоката
   'tags': [ 
      scooters_msk,
      ...
   ], // теги 
   fuel_level, // уровень заряда
   last_heartbeat_time, // время последнего хартбита
   status, // статус самоката
   'firmwares': { // текущие версии прошивок самоката
      'iot_firmware': "1.1.1",
      'gsm_firmware': "2.0.3",
      "audio_lock" : "lock.wav",
      ...
   },
}
```

В эксперименте будут проверки по полям из json выше и эксперимент будет возвращать json:

```
{
   'type': 'type', // тип прошивки, например,iot, audio_full и т.п. вернём none, если не надо обновлять
   'version': 'version', // версия новой прошивки
   's3_url: 'link', // ссылка на S3,
}
```

***Пример***

****Обязательные проверки****

```
fuel_level > 10 &
last_heartbeat_time > current_time - 60 &
status in [available, service]
```

****Условие****

```
type='iot' &
firmwares.iot_firmware >= 1.1.1 & firmwares.iot_firmware <= 1.2.0 &
[scooter_spb, scooter_msk] in tags &
scooter_num >= 1000 & scooter_num <=2000 &
current_time >= '00:00' & current_time <= '06:00'
```

****Значение****

```
{
   'type': 'iot',
   'version': '1.1.2',
   's3_url': 'taxi-scooter-updater-fw.s3.mds.yandex.net/iot/scooters-iot-firmware-0.0.1-20220616131204.tar.gz',
}
```

**Реализация**

***Где храним прошивки***

Храним прошивки в S3. 
https://yc.yandex-team.ru/folders/akun4ts1t82cc7l50521/storage/buckets

Бакеты:

1. taxi-scooter-updater-fw-test (test)
2. taxi-scooter-updater-fw (prod)

Папки в S3:

1. audio
2. battery_lock
3. bluetooth
4. iot
5. iot_ninebot
6. master_controller
7. cable_lock
8. gps

***Как добавляем новую прошивку***

В данный момент просто загружаем файл в S3 в нужную папку.

Далее будет реализована админка, в которой можно будет указать тип прошивки и загрузить файл, который сам загрузится в S3.

***Новые таблицы***

*update_queue*

```
{
   "id": "id",
   "firmware_type": тип прошивки,
   "firmware_version": прошивка,
   "imei": imei,
   "car_id": car_id из car/details
   "scooter_num": номер самоката
   "status": текущее состояние обновления, -1:failed, 0:new, 1:success,
   "error_message": сообщение об ошибке,
   "created_at": дата создания,
   "updated_at": время последнего обновления записи,
}
```

***Какой periodic используем***

*LockedPeriodic* + *STQ*

****LockedPeriodic**** 

Будем использовать LockedPeriodic - так как нам надо, чтобы наша крона выполнялась на одном инстансе периодически.

- У LockedPeriodic есть метод OnConfigUpdate, который вызывается при изменении конфига, так что его легко контролировать с помощью конфига.

- Пример использования:
   https://a.yandex-team.ru/arcadia/taxi/uservices/services/fleet-vehicles/src/workers/periodic_sync_digitalbox.hpp?rev=2cc4d1f485a1379ef9e451933a35802519f6ab4b
   https://wiki.yandex-team.ru/users/chironova/notes/lockedperiodic-pod-postgres/.ru-en

- При инициализации, необходимо заполнить мапу, из ключей из firmwares, и значением 1, то есть

- Необходимо создать таблицу в базе:

*last_used_scooter_to_updating*

```
{
   'type', // firmware_types 
   'number' // последний номер самоката, который обновлялся
}
```

- Будем инициализировать мапу last_used_scooter_to_updating из значений этой таблицу

   Пример:

```
   last_used_scooter_to_updating = {
      'iot' : 100,
      'ecu' : 2222,
      ...
   }
```

****Флоу**** 

1. Проверяем в конфиге enable == true
2. Инициализируем мапу last_used_scooter_to_updating
3. Достаем номера самокатов из car/list
4. Начинаем идти по типам из firmware_types конфига.

   Идём по первому типу (например, firmware_type_1).
5. Достаем все номера самокатов и информацию о них (версии прошивок, теги, статус, уровень заряда и т.д.)
   Дергаем ручку car/details
6. Достаем из таблицы update_queue кол-во stq, которые еще выполняются для данного типа. 
   available_num_for_stq = bulk_count - количество задач.
7. Проверяем, что значение updating_enabled = true

8. Начинаем перебирать самокаты, начиная со следующего номера после last_used_scooter_to_updating[firmware_type_1]
9. Делаем обязательный проверки

   - available_num_for_stq > 0, если нет, то переходим к шагу 14
   - Нет тега updating_firmware (updating_firmware - значит, что уже обновляем самокат)

10. Маппим нейминг прошивок из saas в читаемый вид.

      - mcu_firmware -> iot_firmware
      - gsm_firmware -> ecu_firmware
      - gps_firmware -> gps_firmware
      - ble_firmware_version -> ble_firmware

      Значения справа мы будем использовать при отправке в эксперимент.

11. Отправляем данные самоката в эксперимент и получаем json в ответ.

      - Если code = none, значит обновлять не надо
      - Если вернулся нормальный code и ссылка на S3, то значит что мы должны обновить этот самокат.
         a) Проверяем, что ссылка на S3 корректна, если нет, то информируем о проблеме и переходим к след самокату.
         b) Заводим задачу в stq на обновление самоката, передаем car_id, url, firmware_type, stq_retries
         c) Уменьшаем счетчик available_num_for_stq
         d) Обновляем last_used_scooter_to_updating[firmware_type_1]
         e) Добавляем новую запись в update_queue со статусом new (0) !

12. Переходим к след самокату
    Если его номер совпадает с номером самоката, с которого начинали, или available_num_for_stq=0, то переходим к след. прошивке к шагу *4*.
    Если нет, то переходим к шагу *9*.

13. Если обошли все прошивки, то заканчиваем перебор
14. Сохраняем новые значения last_used_scooter_to_updating в БД


****STQ****

В STQ мы будем обновлять прошивку конкретного самоката.

****Флоу**** 

1. Достаем информацию о самокате из car/details
2. Проверяем, что на нем нет тега updating_firmware
   Если есть, то надо ставить задачу в очередь заново
   Если попыток >= stq_retries, то снимаем тег updating_firmware и ставим статус failed (-1) + сообщение ошибки.
3. Добавляем тег updating_firmware
4. Отправляем запрос на обновление в ручку car_control и ждем выполнения

При вызове ручки надо учитывать следующий маппинг:

```
VEGA_MCU_FIRMWARE_VERSION = 2  # IoT Firmware
VEGA_GSM_FIRMWARE_VERSION = 3  # Scooter Firmware: ECU Driver Firmware
BLE_EXT_BOARD_APP_VERS = 33002  # BLE Firmware
VEGA_GPS_FIRMWARE_VERSION = 4  # GPS firmware
VEGA_TX_DATA_SERV1 = 2008  # Scooter domain url
AUDIO_FILE_SENSOR = 1172
AUDIO_LOCK_SUBID = 2
AUDIO_LOCATE_SUBID = 3
AUDIO_UNLOCK_SUBID = 5
AUDIO_BATTERY_LOW_SUBID = 10
AUDIO_FULL_PACKAGE = 999
```

- Если ошибка:

   a) проверяем, что если это была попытка < stq_retries, то:
      - Cтавим задачу в очередь повторно

   b) Если >= stq_retries, то значит какие-то проблемы сейчас с обновлением:
      - Обновляем запись в update_queue, ставим статус failed (-1)

- Если удачно:
   - Обновляем запись в update_queue, ставим статус success (1)
   - Обновляем версию прошивки в таблице scooters (пока не доступно)

5. Снимаем тег updating_firmware.

Полезные ссылки:
1. https://wiki.yandex-team.ru/taxi/backend/architecture/stq
2. https://wiki.yandex-team.ru/taxi/backend/userver/tasks
