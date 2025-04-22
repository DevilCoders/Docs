При необходимости, в Атласе можно использовать ноду. Сейчас такой необходимости нет, так что и в проде ноды нет.

## Разработка

1. Код лежит в папке `server`
2. Запуск из ./server `npm run start:dev`

Note: если нода стартует нормально, но при тесте бэка (https://taxi-atlas.eugenest.front.taxi.dev.yandex-team.ru/node-api/ping, например) ловите 503, то, возможно, надо поменять овнера у .sock-файла (taxi-atlas-node-api.eugenest.sock в моём случае): `sudo chown www-data:www-data taxi-atlas-node-api.eugenest.sock`.  

## Выкатка

Образы лежат тут _registry.yandex.net/taxi-atlas/taxi-atlas-node_, адекватный на текущий момент — **1.1.3**

Пока не настроена сборка отдельных компонентов в тимсити, собираем через `./qloud/ideploy.sh -> node`

Подёргать можно так:

![](https://jing.yandex-team.ru/files/eugenest/Снимок%20экрана%202020-04-10%20в%2012.20.08.png)

Note: версия енва хранится в QLOUD_ENVIRONMENT (testing / stable) 

В Qloud роут и компонент выглядят так:

![](https://jing.yandex-team.ru/files/eugenest/2020-04-10T09%3A22%3A58Z.png)

Рабочая версия в этом драфте: https://qloud-ext.yandex-team.ru/projects/taxi-tools/atlas/testing?version=1586509716823

Note: там можно попробовать работу вебсокетов:

![](https://jing.yandex-team.ru/files/eugenest/2020-04-10T09%3A26%3A39Z.png)

Но что-то не так с конфигом qloud — рвётся подключение, общение фолбэчится на http.

**UPDATE**: в этом драфте https://qloud-ext.yandex-team.ru/projects/taxi-tools/atlas/testing?version=1586511662325 это пофикшено на уровне настроек nginx в /node-api роуте:

![](https://jing.yandex-team.ru/files/eugenest/Снимок%20экрана%202020-04-10%20в%2012.50.30.png)
