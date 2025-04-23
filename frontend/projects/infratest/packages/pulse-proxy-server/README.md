# Reviser Proxy server

```
npm i
node proxy.js
```

### Как работает

Браузер ходит через специальный кеширующий прокси 127.0.0.1:8009. Прокси дампит статические ресурсы на диск. На последующих запросах прокси отдает дампы статических файлов сразу, без похода по сети.

### Пример

Запускаем прокси

```
node proxy.js
```

Запускаем Chrome Headless как-то так:

```
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --proxy-server="127.0.0.1:8009" --ignore-certificate-errors https://yandex.ru/search/?text=madonna
```

**Обязательные флаги для Chrome Headless**

--ignore-certificate-errors
--proxy-server="127.0.0.1:8009"


### Сертификаты и ключи

Генерировать сертификат и ключ с помощью пакета `anyproxy-ca`

### Опции:

Через переменные окружения можно конфигурировать запуск прокси

- DUMPS_DIR – Папка на диске где будут лежать дампы статических файлов (Default: `./dumps/`)
- STRICT_MODE – Бросает ошибку если нет дампа на диске (Default: `0`)
