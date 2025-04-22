## Библиотека для подключения checkouter-client

1. ```ru.yandex.market.adv.config.CheckouterApiAutoconfiguration``` - автоконфигурация для подключения
   checkouter-client.

## Подключение checkouter-client

1. Конфигурация для создание описана в ```ru.yandex.market.adv.config.CheckouterApiAutoconfiguration``` и повторяет
   ```checkouter-client/WEB-INF/checkouter-client.xml```. Так сделано, чтобы не переопределять bean-ы, которые уже есть
   в контексте приложения.
2. Весь перечень настроек проекта Можно посмотреть в
   классе ```ru.yandex.market.adv.properties.CheckouterApiProperties```.

## URL

### Для тестинга

1. ```market.checkouter.client.https.url=https://checkouter.tst.vs.market.yandex.net:39011/```
2. ```market.checkouter.client.url=http://checkouter.tst.vs.market.yandex.net:39001/```

### Для прода

1. ```market.checkouter.client.url=http://checkouter.market.http.yandex.net:39001/```
2. ```market.checkouter.client.https.url=https://checkouter.market.http.yandex.net:39011/```

## Информация по checkouter

[Документация](https://wiki.yandex-team.ru/market/marketplace/dev/checkouter/)
