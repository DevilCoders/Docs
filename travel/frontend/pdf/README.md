# Yandex Travel Generate PDF

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/pdf&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/pdf)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/pdf&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/pdf)

Приложение для генерации ваучера заказа отелей и автобусного билета.
Приложение недоступно снаружи и живет только в рамках сети Яндекса.

## ручки

### /pdf/generate - синхронная генерация отельного ваучера (нужно будет удалить)

-   method: GET
-   query:
    -   orderId: id заказа
    -   fileName: название файла, с которым сохранить в s3
-   response: { filePath: путь до файла в s3 }

### /pdf/generateHotelVoucher - генерация отельного ваучера

-   method: POST
-   body:
    -   orderId: id заказа
    -   fileName: название файла, с которым сохранить в s3
-   response: пустой. Статус 200, если генерация запустилась

### /pdf/generateBusesTickets - генерация автобусного билета

-   method: POST
-   body:
    -   orderId: id заказа
    -   fileName: название файла, с которым сохранить в s3
-   response: пустой. Статус 200, если генерация запустилась

### /pdf/generateHotelBusinessTripDoc - генерация документов после командировки в отельном заказе

-   method: POST
-   body:
    -   orderId: id заказа
    -   fileName: название файла, с которым сохранить в s3
-   response: пустой. Статус 200, если генерация запустилась

### /pdf/state - статус сгенерированного файла

-   method: GET
-   query:
    -   fileName: название файла
-   response: { url: путь до файла в s3, lastModified: временная метка последнего изменения файла }

## Переводы

[Tanker](https://tanker-beta.yandex-team.ru/project/ya_travel_pdf)

## Разработка

1. Устанавливаем все пакеты `npm ci`.
2. Копируем файл с переменными окружения `cp .env.development.example .env.development`
3. Запускаем проект `start:dev:remote`.
4. Пример конфига `nginx`.
   Конфиги common/ssl и common/gzip создайте по [инструкции](https://ui.yandex-team.ru/dev-server#nastrojka-nginx).

```
server {
    include common/ssl;
    include common/gzip;

    server_name ya-travel-pdf.${user}.ui.yandex.ru;

    set $projectPath /home/${user}/projects/ya-travel-pdf;
    set $projectBuildPath $projectPath/build/;
    set $nodeStartPort 9000;

    # Logs #

    access_log /home/${user}/nginx-logs/travel-pdf/travel-pdf.access.log;
    error_log /home/${user}/nginx-logs/travel-pdf/travel-pdf.error.log;

    # Root #

    location / {
        try_files $uri @node;
    }

    # Static files #

    location /static/assets/ {
        alias $projectBuildPath/client/;
    }

    location /static/ {
       alias  $projectPath/public/;
    }

    # Render Server #

    location @node {
        proxy_pass http://127.0.0.1:$nodeStartPort;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_redirect off;
    }
}

```

5. Запускаем приложение командой: `npm run start:dev:remote`
6. Выставляем переменную окружения S3_ROBOT_CREDENTIALS в .env.development для успешной загрузки файлов в s3. (см. .env.development.example)

## Настройка TVM

Есть [автоматизированный способ](tools/tvm/README.md) настройки tvm с помощью bash скриптов.

Либо если не получится вариант через скрипты, то можно настроить tvm [самостоятельно](docs/tvm.md).

Полезно настроить автостарт

```
$ sudo systemctl enable yandex-passport-tvmtool
```

## Запуск Puppeteer на Unix

Потребуются некоторые [зависимости](https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md#chrome-headless-doesnt-launch-on-unix)

```
sudo apt-get update
```

```
sudo apt-get install -y ca-certificates fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgbm1 libgcc1 libglib2.0-0 libgtk-3-0 libnspr4 libnss3 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 lsb-release wget xdg-utils
```

## Deploy

[Deploy](https://deploy.yandex-team.ru/projects/travel-frontend-pdf)

### Testing

https://travel-tools-test.yandex.net

[Балансировщик](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/show/)

### Production

https://travel-tools.yandex.ru

[Балансировщик](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-prod-internal-balancer/show/)

## Мониторинги и дашборды

[Дашборд](https://datalens.yandex-team.ru/huurcsd89uwse-travel-frontend?tab=yZa)

## Список алертов Golovan

| Мониторинг       | Production                                                                                         |
| ---------------- | -------------------------------------------------------------------------------------------------- |
| **5xx ошибки**   | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_pdf_production_response_5xx_ydeploy) |
| **CPU Usage**    | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_pdf_production_cpu_usage_ydeploy)    |
| **Disk Usage**   | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_pdf_production_disk_usage_ydeploy)   |
| **Memory Usage** | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_pdf_production_memory_usage_ydeploy) |

## Доставка кода

Кто-то пересылает свой код средствами IDE, здесь описан альтернативный способ с помощью rsync.
Подразумевается, что локально уже установлен rsync, на UNIX-based ОС, как правило, он уже установлен.
Для windows потребуется установить порт bash'a, а потом сам rsync. После этого:

1. Создать в корне проекта файл `.rsyncpath` (Он уже добавлен `.gitignore`).
2. В файл положить такую строку `<user>@<user>.ui.yandex.ru:<path-to-project>`.
   Пример: `nskulikov@nskulikov.ui.yandex.ru:/home/nskulikov/ya-travel/`
3. Локально запустить команду `npm run watch`.
