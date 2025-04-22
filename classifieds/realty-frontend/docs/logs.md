# Логи

## Клиентские логи

### Яндекс.Метрика

Используется для бизнес аналитики. Чтобы посмотреть в [проде](https://metrika.yandex.ru/) нужно запросить [роль в IDM](https://idm.yandex-team.ru/) к узлу `Метрика -> Доступ к счетчику сервиса Яндекса`.
[Документация](./metrika.md) по использованию у нас в проекте

### Rum.Errors

Логируем браузерные ошибки пользоватлей. Смотрим в [error-booster](https://error.yandex-team.ru/projects/realty/projectDashboard).
Подключаем [тут](https://github.com/YandexClassifieds/realty-frontend/blob/master/realty-core/app/lib/rum-error-counter/index.js)

### Front log/tskv log/старое логирование

Используется для бизне аналити и ML. Реализация отпрвки в [StatAPIMixin](https://github.com/YandexClassifieds/realty-frontend/blob/master/realty-core/app/controller/mixin/stat_api.js).
Логируем через методы хоков [withStats и withGateStats](https://github.com/YandexClassifieds/realty-frontend/blob/master/realty-core/view/react/modules/metrics/enhancers/withStats.js#L71)
Посмотреть можно в [yql](https://yql.yandex-team.ru/Operations/YIJ3Mb94hv4LoFdBra9sfZwAsUdt52A9eik2VzZ0bcg=) или [hue](https://hue.vertis.yandex.net/) `logs.realty_front_log`

#### Полезные ссылки
- [push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client/)
- [Конфигурация push-client](https://wiki.yandex-team.ru/logbroker/docs/push-client/config/)
- [Logbroker](https://logbroker.yandex-team.ru/docs/)
- [Logfeller](https://wiki.yandex-team.ru/logfeller/)
- [Как все это подключить](https://wiki.yandex-team.ru/logfeller/connection/)
- [Конвенция работы с топиками](https://wiki.yandex-team.ru/vertis-admin/vertis-lb-convention/)

#### За что мы отвечаем

- Конфиг для `push-client`. Находится в нашем проекте, в `docker/run-push-client.sh`;
- Настройку топиков в логброкере. Осуществляется через консольную утилиту `logbroker`;
- Настройку режима индексации и сборки, парсеры для наших логов в `logfeller`.

#### Список наших топиков в logbroker

- vertis/realty/prod/front-log
- vertis/realty/test/front-log

#### Список наших таблиц в YT
- [vertis-realty-prod-front-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/vertis-realty-prod-front-log)
- [vertis-realty-test-front-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/vertis-realty-test-front-log)

### Новое логгирование/realty3.event
Используется для бизнес аналитики и ML. Реализация в [StatAPIMixin](https://github.com/YandexClassifieds/realty-frontend/blob/master/realty-core/app/controller/mixin/stat_api.js).
Логгируем как и старое логированние через методы хоков [withStats и withGateStats](https://github.com/YandexClassifieds/realty-frontend/blob/master/realty-core/view/react/modules/metrics/enhancers/withStats.js#L71), данные складываются в  поле `newLog`.
Посмотреть можно в [yql](https://yql.yandex-team.ru/Operations/X9NlezzwiJJdz15bI1vrAgyTVlUuhWyCPoeBgq4Gb9s=)

## Серверные логи

В тестинге и проде пишутся в stdout и stderr, поставляются в clickhouse и yt, см. примеры типовых запросов и
документацию админов. В деве пишутся в файлы.

[Примеры типовых yql запросов](https://wiki.yandex-team.ru/users/romanpoleguev/zaprosy-v-logax/)  
[Документация админов](https://wiki.yandex-team.ru/vertis-admin/logs/)

### Расположение в деве

```
tail -f <директория_проекта>/log/<название_лога>.log
```

### Виды логов
- `debug.log` – Логи приложения (stdout)  
- `error.log` – Ошибки приложения (stderr)
- `realty-front.log` - Логи для записи событий для статистики (продуктовые логи).
