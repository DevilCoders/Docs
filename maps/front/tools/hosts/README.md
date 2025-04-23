# hosts/inthosts
## Общая информация
| Название   | Значение
| -----------| ------------------------------------
| Стартрек   | https://st.yandex-team.ru/MAPSINFRA

## Схема конфигов обычного проекта
Подавляющее большинство фронтенд сервисов используют разные конфиги в зависимости от окружения.

Обычная схема проектных конфигов следующая:
```
configs\
    current -> development\
    development\
    testing\
    production\
```
где `current` — это симлинка на текущее окружение.

По умолчанию симлинка `current` чаще всего устанавливается на девелоперские конфиги.

## Проверка значений в конфигах
Хосты из всех окружений проверяются по json схеме. Хост должен присутствовать в конфигах для всех окружений. Если хост для какого-то окружения пока не доступен, то допускается указать значение `null`.

Для проверки значений используется три форматера:

  * `url` — для проверки урлов
  * `url-template` — для проверки темплейтов вида `https://lrs.maps.yandex.net/tiles?l=sta&%c&tm=%v&%l`
  * `key` — для проверки ключей для тайлов вида `%c&l=stj&tm=%v`

## Sandbox ресурсы

Для приложений, живущих в облаках, были созданы два типа ресурсов: [MAPS_CONFIG_HOSTS](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=MAPS_CONFIG_HOSTS) и [MAPS_CONFIG_INTHOSTS](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=MAPS_CONFIG_INTHOSTS).

Подробнее про использование этих ресурсов в ваших приложениях читайте [документацию](https://wiki.yandex-team.ru/maps/dev/ui/deploy/yd/#resources).

## Загрузка конфигов на сервисе
Для работы с конфигами используем модуль [ymaps-host-configs](https://github.yandex-team.ru/maps/ymaps-host-configs).

## Переопределения конфигов
### Переопределение через конфиг на файловой системе
По умолчанию при запросе ищется конфиг для переопределения на файловой системе. Этот способ используется в двух случаях:

  * подменить конфиги для разработческой копии сервиса;
  * поднять enterprise-версию API или долгоживующие стенды.

Ниже все примеры представлены для `inthosts`. Для `hosts` — все аналогично.

#### development
  * Дефолтный конфиг берётся из [hosts-testing.json](inthosts/1.1/hosts-testing.json).
  * Переопредления конфигов будут браться из домашней директории: `$HOME/.inthosts/%host%.json`
  * Значения из кастомного конфига переопределяют значения из дефолтного.

#### testing
  * Дефолтный конфиг берётся из [hosts-testing.json](inthosts/1.1/hosts-testing.json).
  * Кастомный конфиг ищется в [testing/%host%.json](inthosts/1.1/testing).
  * Значения из кастомного конфига переопределяют значения из дефолтного.
  * Для добавления кастомного конфига нужно добавить его в пакет, пересобрать и выкатить в тестинг.

#### production
  * Дефолтный конфиг берётся из [hosts-production.json](inthosts/1.1/hosts-production.json).
  * Кастомный конфиг ищется в [production/%host%.json](inthosts/1.1/production).
  * Значения из кастомного конфига переопределяют значения из дефолтного.
  * Для добавления кастомного конфига нужно добавить его в пакет, пересобрать и выкатить в продакшен.

### Переопределение через параметр host_config
Переопределение с помощью конфигов на файловой системе имеет один существенный недостаток — это необходимость перевыкладывать пакеты после добавления конфигов. Выкладка пакетов с хостами медленная, т.к. пакет устанавливается на несколько кластеров.

Для того, чтобы облегчить переопределение конфигов для разработческих нужд, была добавлена поддержка переопределения хостов с помощю query-параметра `host_config`.

Поддержка `host_config` добавлена в следующие сервисы:
  * [верстка карт](https://wiki.yandex-team.ru/maps/dev/ui/products/maps/)
  * [API Яндекс.Карт](https://tech.yandex.ru/maps/doc/jsapi/2.1/quick-start/tasks/quick-start-docpage/)
  * [http-сервисы](https://wiki.yandex-team.ru/maps/dev/ui/http-services/)
  * [jsapi-сервисы](https://github.yandex-team.ru/mapsapi/jsapi-services)

Т.к. самым частым кейсом является добавление переопределений для верстки карт, то будем рассматривать именно ее.

Для добавления переопределения необходимо делать запрос верстки вида:
```
https://l7test.yandex.ru/maps?host_config[inthosts][<inthost>]=<value>&host_config[hosts][<host>]=<value>
```
где
  * `<inthost>` — ключ из [inthosts/1.1/hosts-testing.json](inthosts/1.1/hosts-testing.json)
  * `<host>` — ключ из [hosts/1.3/hosts-testing.json](hosts/1.3/hosts-testing.json)
  * `<value>` — переопределние хоста/интхоста

**Важно.** Такое точечное переопределние конфигов работает только в тестинге.

Если для какого-то хоста сделано много переопределений, то можно задать нужный "пресет" с помощью `host_config[hostname]=<value>`. Такой способ переопределения будет работать и в тестинге, и в продакшене.
```
https://l7test.yandex.ru/maps?host_config[hostname]=search-test.maps.yandex.ru
```

При переопределении через `hostname` будут использоваться [конфиги с файловой системы](#Переопределение-через-конфиг-на-файловой-системе).

#### Примеры
##### Переопределение хоста метапоиска
```
https://l7test.yandex.ru/maps?host_config[inthosts][search]=http://bering.yandex.ru:8999/
```

##### Переопределение меты
```
https://l7test.yandex.ru/maps/?host_config[inthosts][meta]=http://meta-int.lback01g.tst.maps.yandex.ru/
```

##### Переопределение маршрутизатора ОТ
Верстка карт ходит в маршрутизатор через API, поэтому необходимо еще поменять апи на дататестинговое.
```
https://l7test.yandex.ru/maps/?host_config[hosts][api]=https://api01h.dtst.maps.yandex.ru/&host_config[apiRouteService]=https://api01h.dtst.maps.yandex.ru/services/route&host_config[inthosts][masstransit]=http://mt-router01h.dtst.maps.yandex.ru/mtroute/
```

## Как поменять конфиги hosts или inthost
см. [CONTRIBUTING.md](CONTRIBUTING.md)
