# express-national-redirect

Миделвара для редиректа на национальный домен с учетом куки yandex_gid, IP-адреса пользователя и куки yp.

## Установка

Установить NPM-пакеты
```bash
npm install express-national-redirect cookie-parser express-tld --registry=http://npm.yandex-team.ru/
```

Установить DEB-пакеты с биндингами для geobase и langdetect
```bash
apt-get install libyandex-lang-detect yandex-lang-detect-nodejs yandex-lang-detect-data yandex-libgeobase{5,6}-default libgeobase{5,6}-nodejs
```

## Пример
```ts
import express from 'express';
import expressTld from 'express-tld';
import cookieParser from 'cookie-parser';
import expressNationalRedirect from 'express-national-redirect';

const app = express();

// Для точного определения ip адреса пользователя
app.enable('trust proxy');

// Для парсинга tld
app.use(expressTld());

// Для поддержки кук yandex_gid и yp
app.use(cookieParser());

app.use(expressNationalRedirect({
    // Required
    app: {
        domains: ['ru', 'ua', 'by', 'kz', 'com', 'com.tr', 'net']
    },

    // Required
    geobase: {
        version: 6, // Возможно использовать 5 и 6 версии геобазы
        options: {
            geobaseData: '/var/cache/geobase/geodata6.bin'
        }
    },

    // Optional path to langdetect data
    langdetect: {
        data: '/usr/share/yandex/lang_detect_data.txt'
    },

    // Optional bunyan-compatible logger (ex. yandex-logger)
    logger: bunyan.createLogger({ name: 'mw.national-redirect' })
}));
```

## Разработка

```bash
# Запуск тестов
npm test
```
