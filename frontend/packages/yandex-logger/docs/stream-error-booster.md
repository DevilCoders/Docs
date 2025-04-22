# yandex-logger стрим для логирования в Error Booster

Стрим для yandex-logger, позволяющий писать логи в Error Booster двумя методами: через свой unified agent или через стандартный сайдкар [Logbroker](https://deploy.yandex-team.ru/docs/concepts/pod/sidecars/logs/logs) для поставки логов.

## Свой unified agent
Для связи с Error Booster'ом используется [unified agent](https://logbroker.yandex-team.ru/docs/unified_agent) и [unix-dgram](https://github.com/bnoordhuis/node-unix-dgram).

### Схема
![Схема](https://jing.yandex-team.ru/files/savichev/Схема.jpg)

yandex-logger с помощью модуля unix-dgram отправляет логи в unix-socket, который слушает Unified Agent,
последний же в свою очередь отправляет логи в Log Broker,
откуда Error Booster читает логи из вашего топика и отображает их в своём интерфейсе.

### Подключение

1. Создать топик в Log Broker: [инструкция](https://wiki.yandex-team.ru/error-booster/error-how-to/#kakpodkljuchitsja)

2. Добавить в ваш образ с приложением Unified Agent удобным для вас способом: [инструкция](https://logbroker.yandex-team.ru/docs/unified_agent/installation)

3. Получить oAuth-токен для Log Broker: [инструкция](https://logbroker.yandex-team.ru/docs/unified_agent/quickstart#poluchenie-oauth-tokena-dlya-dostupa-v-logbroker)

3. Подготовить конфиг для Unified Agent:
```yaml
status:
  host: '::'
  port: 16301

routes:
  - input:
      plugin: syslog
      config:
        path: /tmp/unified.sock
        max_message_size: 10240

    channel:
      output:
        plugin: logbroker
        config:
          endpoint: logbroker.yandex.net
          # Здесь должен быть указан путь до топика, который был создан на 1 шаге
          topic: /account/topic
          oauth:
            secret:
              # Путь до env переменной, где хранится значение oAuth-токена
              env: LOGBROKER_OAUTH_TOKEN

```

4. Запустить рядом с вашим приложением Unified Agent:
```shell
/resources/unified_agent --config /app/unified-agent/config.yml
```

5. Подключить стрим в приложении:
```js
const logger = require('@yandex-int/yandex-logger')({
    streams: [
        {
            level: 'warn',
            stream: require('@yandex-int/yandex-logger/streams/error-booster')({
                // Название проекта, в scope которого складывать ошибки. Проект будет доступен на витрине https://error.yandex-team.ru/projects
                project: 'yours-project',
                // Путь до сокета unified_agent'а
                socketPath: '/tmp/unified.sock',
            })
        }
    ]
})
```

## Сайдкар LogBroker
Для связи с Error Booster'ом используется стандартный сайдкар [Logbroker](https://deploy.yandex-team.ru/docs/concepts/pod/sidecars/logs/logs) для поставки логов и [got](https://github.com/sindresorhus/got/tree/v8.3.2).

### Схема
yandex-logger с помощью модуля got по http отправляет логи в LogBroker,
откуда Error Booster читает логи и отображает их в своём интерфейсе.

### Подключение

1. Включить поставку логов и иметь версию `unified agent` не старее чем `22.01.2022 2739742779`

1. Подключить стрим в приложении:
```js
const logger = require('@yandex-int/yandex-logger')({
    streams: [
        {
            level: 'warn',
            stream: require('@yandex-int/yandex-logger/streams/error-booster')({
                // Название проекта, в scope которого складывать ошибки. Проект будет доступен на витрине https://error.yandex-team.ru/projects
                project: 'yours-project',
                // тип сокета: http - для корректной работы этой версии
                socketType: 'http',
                // хост logbroker (по умолчанию localhost)
                socketHost: process.env.ERROR_BOOSTER_HTTP_HOST || 'localhost',
                // порт SYSLOG HTTP input port из https://deploy.yandex-team.ru/docs/concepts/pod/pod#set-i-dostupnye-porty (по умолчанию 12522)
                socketPort: process.env.ERROR_BOOSTER_HTTP_PORT || 12522,
                // полный путь до error-booster из https://clubs.at.yandex-team.ru/infra-cloud/2587 (по умолчанию /errorbooster)
                socketPath: '/errorbooster',
                // максимальное количество сокетов на агент
                // https://nodejs.org/dist/latest-v16.x/docs/api/http.html#agentmaxtotalsockets (по умолчанию 8)
                maxTotalSockets: 8,
            })
        }
    ]
})
```

## Поддерживаемые поля

Все поля описаны [здесь](https://wiki.yandex-team.ru/error-booster/error-how-to/#kakispolzovat).

По умолчанию стрим сам инициализирует следующие поля и не даёт их переопределить:
* **record.additional** - это объединение полей `config.fields.additional` и поля `record.additional`
* **record.pid** - id процесса (`process.pid`)
* **record.dc** `(os.hostname().match(/\bsas|vla|man|iva|myt\b/) || [])[0]`
* **record.host** - `os.hostname()`
* **record.language** - `nodejs`
* **record.level** - уровень логирования
* **record.project** - `config.project`
* **record.msg** - указывается явно через интерфейс логирования, либо берётся из `err.message`
* **record.timestamp** -  `(new Date()).getTime()`

Все остальные поля можно переопределять через стандартный [интерфейс логирования](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/yandex-logger#интерфейс-логирования).

## Пример подключения на примере проекта tap-backend в Deploy с помощью кастомного unified agent

1. Создать топик в Log Broker: [инструкция](https://wiki.yandex-team.ru/error-booster/error-how-to/#kakpodkljuchitsja)

2. Подключаем статический ресурс с Unified Agent: [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/.config/deploy/.yd_tmpl_production.yml#L97)

3. Указываем точку монтирования ресурса: [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/.config/deploy/.yd_tmpl_production.yml#L113)

4. Создаём секрет с oAuth-токен для Log Broker и прокидываем его в переменные окружения в Deploy: [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/.config/deploy/.yd_tmpl_production.yml#L140)

5. Настраиваем политику запуска workload'а с Unified Agent: [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/.config/deploy/.yd_tmpl_production.yml#L154)

6. Настраиваем политику остановки workload'а с Unified Agent, чтобы гарантированно отправить все ошибки в Log Broker, перед выкаткой новой версии приложения [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/.config/deploy/.yd_tmpl_production.yml#L160)

7. Настраиваем [readiness пробу](https://wiki.yandex-team.ru/deploy/docs/concepts/pod/workload/probes/#readiness), которая проверяет готовность Unified Agent, перед тем как пустить трафик на pod: [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/.config/deploy/.yd_tmpl_production.yml#L145)

8. Копируем bash-скрипты и конфиг в Docker-образ с приложением для запуска/остановки Unified Agent: [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/Dockerfile#L37)

9. Подключаем стрим: [пример](https://github.yandex-team.ru/search-interfaces/frontend/blob/e374f255fcded587357941f7b7f1336fba15d582/services/tap-backend/src/lib/logger.ts#L80)

10. Идём в [интерфейс](https://error.yandex-team.ru/projects/tap-backend) Error Booster и проверяем, что всё работает
