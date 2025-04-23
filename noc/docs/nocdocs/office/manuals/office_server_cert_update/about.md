# Обновление замена сертификатов для офисных серверов

| Автор | Контакт |
|:-----:|:-------:|
| Александр Пинтаев | [apintaev](https://staff.yandex-team.ru/apintaev) |

--------------

## Сертификаты(мини теория)

Для успешной работы vpn-сервисов и авторизации dot1x на региональном офисном рутере должны быть установлены валидные сертификаты, укомплектованные приватными ключами. Типичный офисный рутер содержит две сущности, для которых нужны сертификаты: 
- IPSEC-туннель до vpn-концентратора 
- модуль авторизации радиуса через 802.1X. 

Сертификаты представляют собой файлы формата x509 с раздельно хранимым не шифрованным приватным ключом. На машинах сертификаты расположены в следующих местах:

**Для IPSEC (strongswan)**:
```
сертификат: /usr/local/etc/ipsec.d/certs
ключ: /usr/local/etc/ipsec.d/private
```
в данном случае сертификат назван по имени машины, с расширение .crt, например sudak.crt, ключ же всегда имеет название private.key.

**Для radius 802.1X**:
```
сертификат и ключ :/usr/local/etc/raddb/certs/
```
в данном случае сертификат назван по имени машины, с расширение .pem, например sudak.pem. Ключ тоже назван по имени машины и имеет расширение `.key`, например `sudak.key`. Кроме того для `radius-а` необходимо создать симлинки `radius.cert` и `radius.key`, указывающие на сертификат и ключ соответственно.

## Просмотр сертификата и сравнение его с ключом

Если возникает необходимость просмотреть сертификат в читаемом виде, то это можно сделать командой:
```
openssl x509 -text -noout -in certname.pem
```
Просмотр ключа:
```
openssl rsa -text -noout -in keyname.key
```
Чтобы убедиться, что ключ соответствует данному сертификату нужно сравнить секции modulus в выводе.

## Получение и установка сертификатов

Для Strongswan и RADIUSd требуется получить 2 разных сертификата. Приватные ключи и запросы на оба изготавливаются автоматически при помощи Makefile'ов в директориях`/usr/local/router/strongswan` и `/usr/local/etc/raddb` соответственно.

### Первичное выделение или аварийная замена протухших сертификатов

1. Сгенерить приватный ключ`make generate-private-key`
2. Сгенерить запрос на сертификат`make generate-csr`На выходе сформируется запрос на сертификат, который будет показан в консоли, а также, в случае с сертификатом для RADIUS, скопирован в файл 
   /usr/local/etc/raddb/certs/`hostname -s`.csr
3. Подписать сертификатОткрываем [Сертификатор](https://crt.yandex-team.ru/api/certificate/?type=client-server&ca_name=InternalCA)В форме внизу страницы выбираем 
   type=client-server
   , 
   Ca name=InternalCA
   , поле 
   Desired ttl days
    оставляем пустым, в 
   Request
    вставить содержимое файла запроса сертификата.В ответ форма должна отдать структуру данных, начинающуюся с 
   HTTP 201 Created. 

   Сертификат в BASE64 лежит по ссылке "download2" 
   
   **ВОТ ТУТ**
   
   VVV
   ![https://wiki.yandex-team.ru/noc/duty/poluchenie-zamena-sertifikata-dlja-ofisnyx-serverov/.files/screenshotfrom2021-11-1907-04-13.png](https://wiki.yandex-team.ru/noc/duty/poluchenie-zamena-sertifikata-dlja-ofisnyx-serverov/.files/screenshotfrom2021-11-1907-04-13.png)  
   
   вместе с цепочкой - в файлы на машинах копируется только сертификат, без цепочки.
   
   {% cut "Муки с занзибаром, если кто любит по-острее." %}
   
   Отправить запрос на сертификат на zanzibar, для выписывания сертификата нашим Certificate Authority (CA): 
   - Открыть в браузере ссылку: [https://zanzibar-caint.ld.yandex.ru/certsrv](https://zanzibar-caint.ld.yandex.ru/certsrv) 
   - В поле формы "Base-64-encoded certificate request (CMC or PKCS #10 orPKCS #7):" вставить содержимое файла запроса сертификата. 
   - Выставить переключатель "Client-server template" в положение "Client-server computer with aproval" для Strongswan и "Web-сервер (с подтверждением)" для RADIUSd и openvpn. 
   - В итоге Zanzibar вернет номер запроса, с этим запросом нужно обратиться на pki@ объяснив цель использования сертификата (после отправки письма можно позвонить по 2900). 
   - Затем снова перейти по ссылке [https://zanzibar-caint.ld.yandex.ru/certsrv](https://zanzibar-caint.ld.yandex.ru/certsrv) (обновление страницы приведет к формированию еще одного запроса, что нам не нужно) и выбрать "View the status of a pending certificate request", забрать сертификат в base64 формате. 
   - Это и будет новый файл сертификата в формате x509.
   
   {% endcut %}

4. Установить скаченные сертификаты в данные директории
   ```sh
   /usr/local/etc/ipsec.d/certs/<fishname>.crt  #для strongswan
   /usr/local/etc/raddb/certs/<fishname>.crt  #для RADIUSd
   /usr/local/etc/openvpn/certs/<fishname>.crt #для OpenVPN (неприменимо для наливки обычной рыбки)
   ```
5. Заменить файл(при первичном выделении не надо) сертификата на машине, рестартовать изменный сервис:
   ```sh
   make -C /usr/local/router/strongswan restart #для strongswan
   make -C /usr/local/etc/raddb restart #для RADIUSd
   make -C /usr/local/etc/openvpn restart #для OpenVPN
   ```
   Рестарт strongswan и openvpn нужно производить исключительно в ночное время между 2 и 6 часами ночи по местному для сервера времени, когда количество пользователей минимально. Проверяйте себя при помощи [https://time.yandex.ru](https://time.yandex.ru).
6. Убедиться, что владелец файла с сертификатом для RADIUSd - пользователь freeradius (chown):
```
sudo chown freeradius:freeradius /usr/local/etc/raddb/certs/<имя рыбки>.crt
```

### Обновление сертификата автоматикой

Т.к. все используемые сертификаты получаются через Сертификатор, это позволяет значительно упростить процедуру обновления сертификатов - Сертификатор хранит CSR всех запросов, что делает возможным воспользоваться специальной ручкой для обновления сертификата в его API. Вокруг API написан скрипт, который автоматизирует получение сертификата, на момент написания этого раздела скрипт лежит в `/usr/local/etc/raddb/certs/` и называется update_cert.py:
```
[14:01:32 MSK+0300]root@muksun.yndx.net:
/usr/local/etc/raddb/certs>./update_cert.py --help
usage: update_cert.py [-h] [--force] [--out FILENAME]
                      crt_filename key_filename

Renew existing client-server certificate using it as an authentication factor.
Works only for certs that were signed with CRT as it reuses the same CSR.

positional arguments:
  crt_filename    /path/to/certificate/file
  key_filename    /path/to/key/file

optional arguments:
  -h, --help      show this help message and exit
  --force         By default if a certificate expirates in more than 120 days,
                  renewal is rejected. This option forces renewal.
  --out FILENAME  Filename to store new cert into. By default certificate
                  serial number is being used with '.crt' added at the end
```
Для обновления сертификата скрипту надо передать опциями пути до файлов сертификата и соответствующего ему приватного ключа. На выходе, если всё прошло хорошо, будет создан файл с именем вида `.crt` - (например: `34365C35000200099C1F.crt`).

Примеры использования:

**Radius**
```
sudo -E make -C /usr/local/etc/raddb/certs/ update
sudo /usr/local/etc/raddb/certs/update_cert.py --force --out $(hostname -s).crt.new /usr/local/etc/raddb/certs/$(hostname -s).crt /usr/local/etc/raddb/certs/$(hostname -s).key
sudo cp /usr/local/etc/raddb/certs/$(hostname -s).crt /$(hostname -s)-radius.crt.bak
sudo mv ~/$(hostname -s).crt.new /usr/local/etc/raddb/certs/$(hostname -s).crt
sudo chown freeradius:freeradius /usr/local/etc/raddb/certs/$(hostname -s).crt
sudo openssl x509 -in /usr/local/etc/raddb/certs/$(hostname -s).crt -noout -text -certopt no_subject,no_header,no_version,no_serial,no_signame,no_issuer,no_pubkey,no_sigdump,no_aux,no_extensions
sudo -E make -C /usr/local/etc/raddb restart
```

**Ipsec**
```
sudo -E /usr/local/etc/raddb/certs/update_cert.py --force --out $(hostname -s)-ipsec.crt.new /usr/local/etc/ipsec.d/certs/$(hostname -s).crt /usr/local/etc/ipsec.d/private/private.key
sudo cp /usr/local/etc/ipsec.d/certs/$(hostname -s).crt /$(hostname -s)-ipsec.crt.bak
sudo mv /$(hostname -s)-ipsec.crt.new /usr/local/etc/ipsec.d/certs/$(hostname -s).crt
sudo openssl x509 -in /usr/local/etc/ipsec.d/certs/$(hostname -s).crt -noout -text -certopt no_subject,no_header,no_version,no_serial,no_signame,no_issuer,no_pubkey,no_sigdump,no_aux,no_extensions
sudo -E make -C /usr/local/router/strongswan -DJUST_DO_IT restart
```

**В случае если сертификаты уже протухли, автоматика не работает**

## Отзыв сертификатов

Отозвать сертификат можно несколькими способами:
1. Если имеются права на сертификат через [сертификатор](https://crt.yandex-team.ru/certificates)
2. В противном случае писать на рассылку pki@

-----------

[Источник](https://wiki.yandex-team.ru/noc/duty/poluchenie-zamena-sertifikata-dlja-ofisnyx-serverov/)
