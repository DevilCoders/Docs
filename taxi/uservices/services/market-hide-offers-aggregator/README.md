# Market Hide Offers Runtime Aggregator

## Описание

Микросервис собирающий обновления состояний офферов в режиме реального времени от различных источников (datacamp, indexator, etc).

<br>

Функционально сервис работает следующим образом:

WIP


<br>

## Архитектура

WIP

<br>

## Как разрабатывать микросервис?

### Cредствами ya make
```
cd arcadia/taxi/uservices/services/market-hide-offers-aggregator
ya make # cборка
ya make -tt # сборка + тесты
```

### Cредствами taxi make

Для сборки сервиса использовать:
```
cd arcadia/taxi/uservices
make build-[SERVICE-NAME]
```

Для тестирования сервиса использовать:
```
cd arcadia/taxi/uservices
make test-[SERVICE-NAME]
make utest-[SERVICE-NAME]
make testsuite-[SERVICE-NAME]
```

Для форматирования исходного кода использовать:
```
cd arcadia/taxi/uservices/services/
taxi-format market-hide-offers-aggregator/
```
---
**NOTE:**
Для этой команды используйте Docker образ!

---

Если вы добавили новые библиотеки то необходимо перегенрировать сборочные файлы:
```
cd arcadia/taxi/uservices
make gen-[SERVICE-NAME]
```
---
**NOTE:**
Для этой команды используйте Docker образ!

---

<br>

## Docker образ

1. Вы можете ознакомится с деталями поддержки Docker в [задаче](https://st.yandex-team.ru/MARKETOUT-46028).
2. [Dockerfile](https://st.yandex-team.ru/ajax/v2/attachments/52415349)
3. [docker-run.sh](https://st.yandex-team.ru/ajax/v2/attachments/58176820)
4. [docker-build.sh](https://st.yandex-team.ru/ajax/v2/attachments/52415348)

<br>

## Как подключиться к микросервису?

* через интерфейс [nanny](https://nanny.yandex-team.ru/ui/#/services) выбрать окружение (production/testing)
* у работающего сервиса скопировать доменное имя, например ```vqqikvqgockuwejz.man.yp-c.yandex.net```
* подключиться по ```ssh```

<br>

## Полезные статьи:

1. [Документация](https://wiki.yandex-team.ru/users/vlmarkov/minimarket-hide-offers-microservice-aggregator/)
2. [Дежурства](https://wiki.yandex-team.ru/users/vlmarkov/minimarket-hide-offers-microservice/minimarket-hide-offers-microservice-duty-instruction/)
3. [Корневая задача](https://st.yandex-team.ru/MINIMARKET-187)
