**Скрипт для отправки пуша через metrica-push-api в рамках регресса приложения auto.ru**

Можно отправлять пуш ТОЛЬКО на 1 девайс с диплинком/урлом внутри

**Использование:**
* ```./send_push_metrica.sh -h``` для вывода в консоли подсказок по параметрам
* ```./send_push_metrica.sh -a deeplink``` выбор действия -  одно из следующих значений: url / deeplink
* ```./send_push_metrica.sh -g eec21b64-d970-4bd7-9d5a-3fd3672c8f2a``` ввод GAID девайса  
* ```./send_push_metrica.sh -i 313DB6A-000A-4EA2-8439-1F6467874F5F``` ввод IDFA девайса
* ```./send_push_metrica.sh -d autoru://app/cars/used/sale/123-123``` ввод диплинка/урла который будет открыт в приложении
