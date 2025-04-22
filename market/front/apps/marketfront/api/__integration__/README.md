# Интеграционные тесты для FAPI

---

Интеграционные тесты кладем в файлы хэндлеров<br>
в `<handler_name>/v1/__spec__/index.integraion.js`

## Разработка и локальный запуск

Для разработки и локального прогона тестов нужно запустить кадавр на логрусе,<br>
так как в противном случае не будут работать tvm гранты.

### Запуск рабочей копии кадавра

Скачать [кадавр](https://github.yandex-team.ru/market/kadavrique.git) на логрус и запустить.<br>
`--port` и `--proxy-port` - могут быть любые незанятые порты.

`node ./bin/kadavr.js start "--port" "7777" "--proxy-port" "5678" "--ui-port" "6789"`

### Запуск стенда

Стенд fapi приложения на логрусе запускаем с переменными KADAVR_HOST и KADAVR_PORT.<br>
`KADAVR_HOST` хост кадавра<br>
`KADAVR_PORT` порт соответствует параметру `--proxy-port`

`KADAVR_HOST=localhost KADAVR_PORT=5678 (npm run start / npm run start:debug)`


### Конфигурация dev машины

Для конфигурации хоста fapi и токена есть 2 переменных:<br>
`FAPI_URL` и `FAPI_AUTH_TOKEN`, которые можно передать при запуске npm скрипта,<br>
либо прописать в конфиг запуска тестов.

При работе через локальный (логрусовый) кадавр необходимо передать переменные окружения:<br>
`KADAVR_HOST` - хост кадавра<br>
`KADAVR_PORT` - порт кадавра из параметра `--port`<br>
Для того, чтобы скрипт мог создать сессию и загрузить стор.

Запуск - `npm run integration`

### Полезные ссылки

[Kadavr cookbook](https://wiki.yandex-team.ru/Market/Verstka/KadavrCookBook/)

### Личный опыт локального запуска

##### Для запуска локально на общем стенде https://ipa-test.market.yandex.ru/ с общим кадавриком:

1. Получить OAuth токен для **тестинга** в паспорте.<br>
Т.к. Маркет не зареган в списке приложений - то подойдёт любой валидный от любого зареганного приложения.<br>
Например, https://wiki.yandex-team.ru/market/beru/front/fapi-beru/kak-poluchit-token-dlja-fapi/<br>
Белое фапи при этом использует продовый паспорт, поэтому даже на тестинге в белое фапи надо ходить с продовым токеном OAuth.<br>
В синее фапи - с тестинговым токеном на тестинге.<br>
2. Для запуска теста addUgcVideo с авторизацией:<br>
`FAPI_AUTH_TOKEN="OAuth AAAAXXXXXXXXX" INTEGRATION=true ../node_modules/.bin/jest --preset='./configs/jest/jestConfigCI.js' --color --ci --projects ./ -t addUgcVideo`<br>
Запускать из директории `marketfront/api`

Если тест без авторизации, то запускать можно без получения токена. Например, resolveDeliveryConditions:<br>
`INTEGRATION=true ../node_modules/.bin/jest --preset='./configs/jest/jestConfigCI.js' --color --ci --projects ./ -t resolveDeliveryConditions`

Для обновления снэпшота - убрать `--ci` и добавить `-u`:<br>
`INTEGRATION=true ../node_modules/.bin/jest --preset='./configs/jest/jestConfigCI.js' --color -u --projects ./ -t resolveDeliveryConditions`

Конфиг в вебшторме выглядит как-то так:

![конфиг вебшторма](https://jing.yandex-team.ru/files/lengl/2022-01-14_16-56.png)

#### Для запуска на своём логрусе со своим кадавриком:

1. Поднять кадаврик на логрусе. https://wiki.yandex-team.ru/Market/Verstka/KadavrCookBook/#zapuskservera <br>
Например, подняли его на порте 9196: `node ./bin/kadavr.js start "--port" "9196"` <br>
Кадавр будет доступен по адресу `https://logrus01ed.market.yandex.net:9196` <br>
Проверить можно, открыв `https://logrus01ed.market.yandex.net:9196/ping` - будет ответ **pong**
2. Поднять api на логрусе. <br>
Например: `KADAVR_HOST=localhost KADAVR_PORT=9196 npm run start:debug` <br>
Апи будет доступно по адресу `https://<login>.api.pokupki.logrus01ed.market.yandex.ru`
3. Локально запускаем нужный тест: <br>
```
KADAVR_HOST="logrus01ed.market.yandex.net" KADAVR_PORT=9196 FAPI_URL="https://<login>.api.pokupki.logrus01ed.market.yandex.ru" FAPI_AUTH_TOKEN="OAuth AgAXXXXXXXXXXX" INTEGRATION=true ../node_modules/.bin/jest --preset='./configs/jest/jestConfigCI.js' --color -u --projects ./ -t resolveDeliveryConditions
```

Если вы работаете на на `logrus01ed` а на другом логрусе - конечно нужно поменять логрус в адресах :)

Конфиг в вебшторме выглядит как-то так:

![конфиг вебшторма](https://jing.yandex-team.ru/files/lengl/2022-01-14_16-59.png)
