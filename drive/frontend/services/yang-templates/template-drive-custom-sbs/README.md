﻿### Отладка

Для запуска живой отладки в TTS выполнить:
```
npm i
npm run start
```
Далее открыть в браузере `https://local.yang.yandex-team.ru:9001`.

### Сборка

Для сборки минифицированного бандла выполнить:
```
npm run prod
```
Бандл будет доступен в каталоге `/dist/` в двух версиях: обычной и сжатой.
Чтобы сразу подключать в свойствах проекта Толоки/Янга сжатую версию, нужно перед деплоем на S3 настроить в этом бакете заголовки:

1. `*.gz`: `Content-Encoding: gzip`
2. `*.js.gz`: `Content-Type: application/javascript`
                                                
### Деплой

Для деплоя на S3 выполнить:
```
npm run deploy
```
Предварительно нужно настроить ключи для доступа в `s3.properties`. Подробнее: https://bb.yandex-team.ru/projects/ASSESSMENT/repos/yastatic-s3

### Проблемы и методы их устранения:

**Не отрабатывает npm start**

Пропишите в `/etc/hosts` новый хост: `127.0.0.1 local.yang.yandex-team.ru`.

**Браузер ругается на невалидный сертификат**

Установите сертификат из `/ssl/dev.pem` или положите туда свой.
