# common-sentry-errorbooster

Библиотека для записи в файл событий в формате errorbooster. По сути обертка над Sentry.
Работает через log appender Sentry.

## Использование библиотеки
* Сначала надо подготовить окружение по инструкции https://wiki.yandex-team.ru/error-booster/error-how-to/
* После создания проекта указать в своих properties файлах:
Обязательные поля:
    * `errorbooster.enable=true`
    * `errorbooster.project=`  название проекта, для которого пишем ошибки. Новые проекты создаются автоматически.
    * `errorbooster.outputfilepath=`  путь, по которому будет записываться файлик с json'ами формата ErrorBooster

Дополнительно:
    * `errorbooster.service=` Если в одном проекте несколько сервисов.
    * `errorbooster.platform=` Платформа: desktop|app|tv|tvapp|station|unsupported; алиасы: touch - touch|touch-p
    * `errorbooster.addsentryevent` Добавлять ли в поле additional оригинальный event sentry?
    Тяжелая операция для booster'а
* Добавить в конфигурацию `log4j2.xml` `<Sentry name="SENTRY"/>` и в нужные Logger'ы
`<AppenderRef ref="SENTRY" level="<LEVEL>"/>`, где `<LEVEL>` - нужный уровень логгирования
* Импортируем конфиг`@Import({SentryErrorBoosterConfig.class})`
* Настрваиваем push-client.
Пример конфига ниже. Topic[ident + log_type] и tvm-client-id надо указывать свои.
```
files:
- name: /var/logs/yandex/error-booster-output.log <- Тут должно быть то, что в errorbooster.outputfilepath
  send_delay: 5
  log_type: errorbooster-market-test
  chunk:
    send-server: 1
    send-file: 1
    send-meta:
      slot: 12645

ident: market_sre
logger:
  file: /var/logs/yandex/push-client/market_error_booster.log
  level: 5
  mode:
  - file
network:
  master_addr: logbroker.yandex.net
  proto: pq
  tvm-client-id: xxxxxxx
  tvm-server-id: 2001059
  tvm-secret-file: push-client-tvm-secret-health/client_secret
watcher:
  state: pstate/push-client_market_error_booster
```
Этот конфиг надо класть в conf/push-client/, если речь идет про nanny.

* Настраиваем logrotate. Библиотечка настроена на переинициализацию записи при SIGHUP.
Например вот так:
```
/var/logs/yandex/error-booster-output.log {
    daily
    rotate 7
    compress
    missingok
    notifempty
    delaycompress
    postrotate
        pgrep -f '^MySuperApplication.*' | xargs kill -HUP <- тут надо грепать ваше приложение
    endscript
}
```

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)
