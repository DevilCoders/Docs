# update_cert.sh
### Примеры использования
Если сертификат можно получить сразу, например он выдан тестовым ЦА, запускаем скрипт:
./update_cert.sh -g %conductor_group -p /certs
при необходимости обновляем пакет
```
...
[INFO] require config-monrun-taxi-nginx-sslcert package >= 1.1.0
update config-monrun-taxi-nginx-sslcert package? (y/N)
```
далее скрипт проверяет сертификат и дает ссылки в YAV и CRT. Переходим в CRT, перезаказываем сертификат. Ссылка дается с фильтром по серийнику и имени - удаляем из фильтра серийник и качаем выданый сертификат в диреторию, указаную при запуске скрипта. Возвращаемся в shell и жмём любую кнопку
```
----
[INFO] current certificate: voucher-order-auth.taxi.yandex.net SERIAL sec-... server.pem
         cert_yav: https://yav.yandex-team.ru/secret/sec-....
         cert_crt: https://crt.yandex-team.ru/certificates?serial_number=SERIAL&host=voucher-order-auth.taxi.yandex.net
Press any key to continue 
```
Скрипт предложит добавить новый сертификат в секрет
```
[INFO] redy to add new certificate to https://yav.yandex-team.ru/secret/...
Update secret: sec-...? (y/N)y
```
далее всё, как и при обычном запуске.

### Запуск:
. ./update_cert.sh -g %\<CONDUCTOR GROUP OF SERVERS\> -p \<DIRECTORY WITH NEW CERTIFICATES\>
### Умеет:
(y/N) - действие требует подтверждения
```
. ./update_cert.sh -g %taxi_unstable_atlas_api -p /Users/temox/Documents/tasks/certificates/files
```
- обновлять `config-monrun-taxi-nginx-sslcert` на хостах группы (y/N)
```
[INFO] require config-monrun-taxi-nginx-sslcert package >= 1.1.0
update config-monrun-taxi-nginx-sslcert package? (y/N)y
[INFO] Updating config-monrun-taxi-nginx-sslcert package
```
- получать имена просроченных сертификатов от `config-monrun-taxi-nginx-sslcert`
- на основе полученных имен получает YAV-секрет сертификата, серийный номер CN сертификата
```
[INFO] check expired certificates: 
[INFO] atlas-api.taxi.dev.yandex.net 7F000F9F4EA5D923141953F06C0002000F9F4E sec-01cqcvqcwsj9974h1cz3vb3w7e server.pem
```
- по CN ищет сертификат в указанной дериктории и выгружает его в YAV (y/N)
```
[INFO] try to update certificate using local cert: /Users/temox/Documents/tasks/certificates/files/atlas-api.taxi.dev.yandex.net.pem
-rw-r--r--@ 1 temox  LD\Domain Users  7156 10 Sep 16:06 /Users/temox/Documents/tasks/certificates/files/atlas-api.taxi.dev.yandex.net.pem
[INFO] Experation date of new certificate: Sep 10 12:55:58 2022 GMT. Serial: 7F0018475956AEA113101EDD02000200184759
[INFO] redy to add new certificate to https://yav.yandex-team.ru/secret/sec-01cqcvqcwsj9974h1cz3vb3w7e
Update secret: sec-01cqcvqcwsj9974h1cz3vb3w7e? (y/N)y
[INFO] Upload status: {"secret_version":"ver-01ff7x4g9rhzs2jg0aqh551zy1","status":"ok"}
[INFO] Certificate successfully updated
```
- запускать на хостах `get-secrets.sh` (y/N)
```
run get-secrets.sh on hosts? (y/N)y
[INFO] updating certificate(s)
```
- в зависимости от статуса, отдаваемого `config-monrun-taxi-nginx-sslcert`, по очереди перезапускает nginx на хостах группы (y/N):
```
[INFO] atlas-api-sas-01.taxi.dev.yandex.net: Nginx needs restart with new certificate
Run process of nginx restarting on atlas-api-sas-01.taxi.dev.yandex.net? (y/N)y
```
  - проверяет нет ли активных блокировок 80 и 443 портов. Если есть - не трогает
  ```
  [INFO] get iptruler dump of atlas-api-sas-01.taxi.dev.yandex.net
  ```
  - перед перезапуском закрывает http и https порты, если что-то было не закрыто ранее, iptruler'ом
  - в течении _DOWN_DELAY_ ждет завершения активных соединений
  ```
  [INFO] waiting for connections closing
  ```
  - перезапускает nginx и ждет его поднятия в течении _UP_DELAY_
  ```
Restarting nginx (via systemctl): nginx.service.
[INFO] waiting for starting of nginx
[INFO] check status and open ports
  ```
  - снимает установленные блокировки, если ставил сам
  - отдаёт статус _ssl_certificate_ и nginx
```
[INFO] monrun -r ssl_certificate on atlas-api-sas-01.taxi.dev.yandex.net
ssl_certificate = Certificate status is ok
[INFO] nginx service status on atlas-api-sas-01.taxi.dev.yandex.net
Active: active (running) since Fri 2021-09-10 16:09:10 MSK; 7s ago
Active: active (running) since Fri 2021-09-10 16:09:10 MSK; 7s ago
OK
```
- после перезапуска, с локальной машины делает запрос на CN, получает информацию о сертификате: дату выдачи, дату окончания и серийный номер.
```
[INFO] get hosted certificate outside
notBefore=Sep 10 12:55:58 2021 GMT
notAfter=Sep 10 12:55:58 2022 GMT
serial=7F0018475956AEA113101EDD02000200184759
```
