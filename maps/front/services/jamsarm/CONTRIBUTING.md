## Developing

### Getting started

1. Install Node.js 8.

2. Add following line to your `/etc/hosts`:
```
127.0.0.1       jams-awp2.local.maps.dev.yandex.ru
```

3. Get certificate:
  * Point you browser to `https://golem.yandex-team.ru/certs/`
  * Press "Заказать"
  * Put `*.local.maps.dev.yandex.ru` to textarea
  * Press "Заказать"
  * Save `.pem` as `~/.ssl/local.maps.dev.yandex.ru.pem`
  * Add `YandexInternalRootCA` to your system: https://wiki.yandex-team.ru/security/ssl/sslclientfix/

4. Setup and run project:
```
git clone https://github.yandex-team.ru/maps/jams-awp2.git
cd jams-awp2
npm i
npm start
```

5. Point your browser to `https://jams-awp2.local.maps.dev.yandex.ru:8080` and enjoy.

### Deploy

#### Testing

```
npm run version:patch
```
or
```
npm run version:minor
```

#### Production
```
npm run deploy:production
```
