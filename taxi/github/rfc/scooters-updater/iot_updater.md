

**Какую задачу решаем?**

Нам необходим updater для нашего IoT, который мог бы обновлять бинарники.

Будет отдельный модуль запускаться на IoT-e.

**На чем писать?**

* C++
Все другие модули написаны так же на c++, то можно и Updater писать на с++.

* Bash
Можно написать bash скриптом, так будет быстрее.
Есть пример из камеры.
https://bb.yandex-team.ru/projects/TAXI/repos/signalq2/browse/signalq_updater/shell/updater.sh

**Что надо сделать?**
1. Ручки в бэке
2. Updater для IoT
3. Завести S3
4. Настроить/запросить Teamcity
5. Написать скрипт для сборки через teamcity
Пример: https://bb.yandex-team.ru/projects/TAXI/repos/signalq2/browse/teamcity.sh

Есть 2 различных сценария обновления.
1. Наш IoT
Обновляем бинарники + linux одним образом.
IoT периодически запрашивает обновление через бэк.
Для указания того, что вышла новая версия, будут использоваться эксперименты.

2. Контроллеры и звуки
Обновляем прошивки контроллеров и звуки на всех IoT-ах (китайские версии 1 и 2 и наш IoT).
Запрос на обновление у нашего и китайских IoT-ов будет делаться через админку.
Будет вызываться команда телематики.

**Наш IoT**

***1. Получаем бинарники***

1. Необходимо настроить teamcity на сборку бинарников
Пример teamcity: https://teamcity.taxi.yandex-team.ru/buildConfiguration/SignalQ_BB_Prod_Release?branch=&mode=builds#all-projects
Пример скрипты для teamcity: https://bb.yandex-team.ru/projects/TAXI/repos/signalq2/browse/teamcity.sh

В артефактах будут доступны 3 файла:
a) rootfs (для обновление OTA)
b) *.elf  (для прошивки нового девайса)
с) s3link.txt (содержит ссылку на s3)

Создается архив, состоящий из rootfs + подпись.
Файл подписывается во время билда.

2. Архив с rootfs будут загружаться в s3

Необходимо настроить бакет s3:
a) scooters-firmware

Они будут не доступны из вне, но мы можем создавать временную ссылку в s3, по которой можно будет скачат прошивку из вне.

***2. Добавляем новую прошивку в эксперименты***
1. Создаем эксперимент scooters_updater_firmare
Пример: https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/experiments/show/signal_device_api_binaries/current?active=all&enabled=all&is_technical=all&name=signal

По мере нового билда, будем добавлять новое значение в эксперимент.
Будет только 1 общая версия на весь билд.

```
{
  "version": "0.0.7-1",
  "link": "s3bucket_link_to_file"
}
```

***3. Updater получает и обрабатывает обновление***

1. Раз в N минут Updater будет дергать ручку /scooters-updater/v1/firmware/scooters/check?sn=123&version=1.1.1

   Ручка возвращает json, если есть новая версии для конкретного самоката:
   {
      "version"=>"1.1.2",
      "url"=>"s3link"
   }

   Если обновления нет, то будет приходить пустой json или json с текущей версией прошивки.

   В этой ручке можно подумать, как можно отслеживать, что мы отправили новую версию и ожидаем обновления.
   Например, можно сохранять в таблицу update_queue информацию, что запросили новую версию.

   И потом, когда самокат опять дернет ручку check, но уже с новой версий, будем отмечать, что обновление завершено.
   Либо надо как-то сделать это отдельной ручкой.

2. После получения ссылки, скачиваем архив
3. Архив состоит из 2 файлов - бинарник и подпись:
    - iot.bin
    - iot.bin.sig

4. Проверяем подпись бинарника.
   На IoT-e будет хранится публичный ключ подписи: /etc/ssl/certs/firware.pem
   
   Первоначально этот ключ будет загружаться вместе с первой установкой прошивки.

5. Если подпись файла корректна, то устанавливаем rootfs.

6. Так же будем хранить какой-нибудь общий json файл между Main-логикой и updater-ом, в который Main-логика запишет serial number, 
а Updater будет записывать текущую версию бинарника.

**Прошивки контроллеров и звуки**

Прошивки контроллера и звуки обновляются так же как и раньше, через команды телематики, как для нового iot-a для и для прошлых версий самокатов.
В мейн-логики и hwbus надо поддержать команды обновления прошивок контроллеров.

***1. Создаем новую прошивку***
В админке будет возможность создать новую прошивку.
Создаем новую прошивку, указываем тип обновляемого контроллера или звук.
Файл прошивки/звука загружается в S3 и нам доступна новая прошивка

***2. Вызываем обновление на страничке самокатов***
В админке будет новая страничка со всеми самокатами и версиями прошивок контроллеров и звуков.
Можно будет нажать кнопку обновить самокат, выбрать что хотим обновить и вызовется ручка
/scooters-updater/v1/firmware/scooters/update

В которой мы создадим временную ссылку на S3 и вызовем ручку телематики для обновления прошивки/звуков.

**Таблицы**
Тип hardware_type
```
{
    master_controller,
    cabel,
    batery_controller,
    dashboard_controller,
    audio_lock,
    audio_locate,
    audio_unlock,
    audio_battery_low,
    audio_full,
    iot,
}
```

1. firmwares
```
{
  "id": "id",
  "hardware_type": "тип устройства, значения из hardware_type",
  "version": "Версия прошивки",
  "file_link": "Ссылка на файл в MDS S3",
  "comment": "Доп. информация о прошивке",
  "created_dt" "Дата создания прошивки"
}
```

2. scooters
```
{
  "id": "id",
  "external_id": "id в базе самокатов",
  "version" : "версия самоката, 1,2,3", (1 - первый китайский iot, в)
  "mc_firmware_id": "id прошивки master controller",
  "cabel_firmware_id": "id прошивки cabel",
  "battery_firmware_id": "id прошивки battery",
  "dashboard_firmware_id": "id прошивки dashboard",
  "audio_lock_firmware_id": "id прошивки audio_lock",
  "audio_locate_firmware_id": "id прошивки audio_locate",
  "audio_unlock_firmware_id": "id прошивки audio_unlock",
  "audio_battery_low_firmware_id": "id прошивки audio_battery_low",
  "audio_full_firmware_id": "id прошивки audio_battery_low",
  "iot_firmware_id": "id прошивки yandex iot",
  "firmware_update_dt": "Дата обновления прошивки",
  "firmware_update_time": "Время установки последней прошивки"
}
```

3. update_queue
```
{
   "id": "id",
   "serial_number": serial number самоката
   "scooter_id": id самоката,
   "firmware_id": id прошивки,
   "hardware_type": тип устройства,
   "status": текущее состояние обновления, -1:failed, 0:new, 1:success,
   "created_dt": дата создания,
   "start_update_dt": дата начала обновления прошивки,
   "end_update_dt": конец обновления прошивки,
   "file_url": ссылка на файл прошивки в S3
}
```
4.api_last_responses 
```
{
    serial_number,
    check_at
}
```

**Какие ручки нужны в бэке**
1. /scooters-updater/v1/firmware/scooters/check?imei=123&version=1.1.1
   Проверяет в экспериментах, есть ли обновления для самоката с imei=123 и версии 1.1.1

   Возвращает json вида:
   {
      "version"=>"1.1.2",
      "url"=>"s3link"
   }

   Так же обновляем check_at в таблице api_last_responses для того, чтобы отследить последнее обращение к ручки от самоката.
   
3. /scooters-updater/v1/firmware/
   Создаем новую прошивку.
   
4. /scooters-updater/v1/firmware/list:
   Возвращаем прошивки

5. /scooters-updater/v1/firmware/update-queue:
   Возвращает данные из таблицы update_queue

6. /scooters-updater/v1/firmware/scooters/update:
   Обновляем прошивку контроллеров или аудио самокатов.

6. /scooters-updater/v1/scooters/
  Возвращает все самокаты и информацию об их прошивках

**Какие ключи надо хранить на IoT-e**
1. Публичный ключ подписи: /etc/ssl/certs/yandex.pem

**Как создавать ключ**
1.To Generate Private Key
```
openssl genrsa -out privatekey.pem 2048
```
2. To Sign
```
openssl dgst -sha256 -sign privatekey.pem -out filename.sig filename
```
3. To Generate The Public Key
dgst -verify requires the public key
```
openssl rsa -in privatekey.pem -outform PEM -pubout -out publickey.pem
```
4. To Verify
```
openssl dgst -sha256 -verify publickey.pem -signature filename.sig filename
```

**Полезные ссылки**
1. Updater в SignalQ
https://bb.yandex-team.ru/projects/TAXI/repos/signalq2/browse/signalq_updater
https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/signal-device-api/src/views/v1?rev=9f6cf1f8d3724b0ace892e5795f4293535f90379

2. Updater в колонке
https://a.yandex-team.ru/arc_vcs/yandex_io/services/updatesd?rev=r9253837