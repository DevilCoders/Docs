# Фронтенд сервиса Портал Логистики

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/151/edit/354861/info)

**TBD**

## Установка и разработка

1. Ставим зависимости `npm ci`
2. Идём в [Сертификатор](https://crt.yandex-team.ru/certificates). Жмём "Заказать сертификат". В всплывающем окне указываем: 
    - **CA name** - InternalCA
    - **Тип сертификата** - Для web-сервера 
    - **Хосты** - `localhost.yandex.ru, localhost.yandex.com, localhost.yango.delivery` (копируем прям с запятыми)
    - **ABC-сервис** - Сервисы Такси
  
    Жмем "Заказать" и скачиваем сертификат, копируем сертификат в корень проекта.  
    Секретница, по-умолчанию, отдает ключ и сертификат в одном файле, их нужно разделить. 
    Поэтому копируем полученный файл и оставляем только секцию:
    ```
    -----BEGIN PRIVATE KEY-----
    ...
    -----END PRIVATE KEY-----
    ```
    В другом файле, соответственно, ее **вырезаем**.
3. Запускаем `npm start`. Если нужно запустить только один сервис `npm start -- <service_name>`

## TVM и Эксперименты 3.0

Чтобы, во время разработки, сервер ходил в сервис экспериментов, нужно создать файл `.tvm.json` следующей командой:

    npm run tool:tvm

## react-script

Проект создна на основе `create-react-app`, доступны все возможности из [документации](https://create-react-app.dev/)

### Конфиги

Не большим отличием являются конфиги. Для них используется не `dotenv`, а `configs-overload`. Конфиги общие и для фронта, и для node-сервера.    
В ключе `process.env` находятся переменные окружения, которые подхватит `react-script`.

### Заведение нового сервиса

1. В папке `services` создаем директорию с будущим сервисом.  
    В ней обязательно должы лежать две папки `public` и `src`, в обоих папках должен лежать индексный файл (для примера см. любой из сервисов).
2. Создаем роут в серверном приложении `packages/server/index.js`.  
    Рендер-функция будет доступна в объекте `renders`, в качестве ключа будет название созданного сервиса.
3. В `package.json` добавляем скрипты запуска и билда:
    ```
    "scripts": {
      "start:order": "SERVICE_NAME=order logistics-react-scripts start",
      "build:order": "SERVICE_NAME=order logistics-react-scripts build",
      "build": "... && npm run build:order"
     }
    ```
    > Временная мера, в будущем нужно научится запускать по start, и билдить по build 
4. Чтобы сервис стал доступен на анстейбл/тестинг/продакшен стендах, нужно добавить проксирующий роут в конфиг nginx'a `docker/etc/nginx/locations/200-app.conf`. 

## Логи

- [[server] Продакшен](https://kibana.taxi.yandex-team.ru/goto/2951126837b8a1f22aaeb62826ff8dcb)
- [[server] Анстейбл](https://kibana.taxi.tst.yandex-team.ru/goto/80dc8cf0-7ce7-11ec-b008-d54b94e8a4d3)
- [[ui] /order](https://error.yandex-team.ru/projects/logistics-frontend-order)

## Раскатка на дополнительные unstable стенды
Для раскатки PR кроме unstable доступны 6 дополнительных стендов `unstable_[2-7]` хосты соответственно `logistics-frontend-[2-7].taxi.dev.yandex.ru`. Процесс аналогичен раскатке в unstable, нужно только дополнительно указать Custom stage (стенд) и Custom tasks (имена веток). Если не указывать ветки соберется билд со всеми PR с метками `deploy:unstable` в противном случае соберутся только указанные в Custom tasks ветки

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Генерация типов

В проекте используется генерация типов из бэкендовых .yaml с помощью пакета `taxi-typings`.
Генерация запускается командой `npm run typings`. Данный скрипт поддерживает все аргументы, которые можно использовать с `taxi-typings CLI`, но передавть их необходимо следующим образом `npm run typings -- --scope repo:target`
После генерации запускается скрипт `posttypings`, который проходится по файлам типов с помощью **prettier** и **eslint**

Источники типов содержатся в конфигурационном файле `types.config.json`. Обратите внимание, что большинство источников находятся в **arc** репозитории, соответственно для работы с ними [*Аркадия*](https://docs.yandex-team.ru/devtools/intro/quick-start-guide) должна быть смонтирована.

[Документация пакета taxi-typings](https://github.yandex-team.ru/ktnglazachev/taxi-typings#taxi-typings)
