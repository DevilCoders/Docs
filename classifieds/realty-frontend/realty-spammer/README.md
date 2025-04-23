# realty-front-spammer

Сервис предназначен для отправки email'ов пользователям по инициативе другого сервиса на стороне бекэнда,
который посылает в сервис запросы с данными в формате protobuf.

Для отправки писем используется [sender](https://wiki.yandex-team.ru/sender/) и следующие шаблоны писем в нём:
 * [trigger-filters](https://sender.yandex-team.ru/realty/campaign/22675/overview)
 * [trigger-welcome](https://sender.yandex-team.ru/realty/campaign/21916/overview)
 
## Основная информация

| Service | URL |
|---|---|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-spammer |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-spammer |
| Grafana | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-spammer |

## Хосты
| Environment | URL |
|---|---|
| Testing | http://realty-front-spammer-http.vrts-slb.test.vertis.yandex.net <br> http://realty-front-spammer-${branch}-http.vrts-slb.test.vertis.yandex.net |
| Production | http://realty-front-spammer-http.vrts-slb.prod.vertis.yandex.net |

## Генерация и использование входных данных в protobuf
### Генерация
Как-то так:
```
echo '{ "offersCount":3  }' | node ./tools/to-protobuf-payload.js stats > payload.bin
```

Или так:
```
cat payload.json | node ./tools/to-protobuf-payload.js stats > payload.bin
```

### Использование
```
curl -d @payload.bin  -X POST -H "Content-type: application/octet-stream" "http://localhost:3000/1.0/stats/?email=orion@yandex-team.ru"
```
