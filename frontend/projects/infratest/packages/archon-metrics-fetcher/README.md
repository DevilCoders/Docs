# archon-metrics-fetcher

Компонент `metrics_fetcher` для [Archon](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon).
Может работать как в паре с плагином для hermione [hermione-get-counters](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/hermione-get-counters),
так и отдельно. 
Использовать компонент следует в составе archon команд. 
Например, `kotik` из [archon-renderer-devserver-command](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon-renderer-devserver-command)
или `hermione` из [archon-hermione](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon-hermione).

## Процесс MetricsFetcher

MetricsFetcher представляет собой отдельный процесс с http сервером, который позволят как получить значение счётчиков, так и рассчитать метрики
с помощью [демона метрик](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon-calc-metrics-daemon). 
Процесс постоянно читает файловые логи серверных (blockstat, baobab) и клиентских (redir) счетчиков, а также получает reqans логи от report-renderer через ipbus 
(отправку сообщений выполняет [archon-renderer](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon-renderer)).

MetricsFetcher умеет отвечать на следующие типы запросов:
### getCounters
Получение счетчиков по `reqId`.
### getAllCounters
Получение счетчиков для всех запросов текущего запуска теста (то есть по текущему `testRunId`).
### getMetrics
Получение рассчитанных демоном значений метрик с учетом доехавших на данный момент логов.
### checkMetrics
Проверка соответствия рассчитанных метрик ожидаемым значениям. 
Поскольку счетчики могут пополняться с течением времени, эта проверка реализована через поллинг. 
### clearStorages
Удаление всех накопленных данных.

## Archon компонент MetricsFetcher

Компонент, запускающий MetricsFetcher. Состоит из методов:

* `init`: запуск MetricsFetcher
    * при успешном запуске сервера `init` компонента будет `fulfilled` с объектом, содержащим некоторые входные опции:
        * `port`
        * `checkedMetricsEnable`
        * `checkedMetricsPath`
    * при неуспехе запуска сервера `init` компонента будет `rejected` с ошибкой-причиной
* `shutdown`: отправка SIGINT MetricsFetcher'у
* `terminate`: отправка SIGKILL MetricsFetcher'у

Компонент зависит от следующих компонентов:

* `clickdaemon` - archon компонент для запуска Clickdaemon.
* `renderer` - archon компонент для запуска ReportRenderer.
* `metricsdaemon` - archon компонент для запуска CalcMetricsDaemon. Если компонента нет в графе, то рассчитать метрики будет невозможно.

Компонент может принимать следующие пользовательские опции:

* `port` - number(default: `случайный свободный порт`); порт http сервера MetricsFetcher.
* `logging.logRawMetricsRequest` - boolean(default: `false`); включить создание файла с запросом в демона метрик, логи в котором будут показаны в сыром виде.
* `prepareLogs` - boolean(default: `false`); включить создание архива с запросом в демон метрик и логами демона метрик при несовпадении посчитанных метрик с ожидаемыми.
  Этот архив нужен для отладки проблем на стороне разработчиков демона метрик и самих метрик.
  Путь к архиву будет указан в тексте ошибки.
* `inspect` - boolean(default: `false`); перевести MetricsFetcher в режим отладки.
* `inspectPort` - number(default: `случайный свободный порт`); порт для подключения отладчиком.
* `checkedMetricsEnable` - boolean(default: `false`); включить запись данных о выполненных в тестах проверках метрик.
  Нужно для сбора статистики о проверках. Заметно замедляет прогон.
* `checkedMetricsPath` - string(default: `'hermione-report'`); путь к директории (относительно CWD), в которой необходимо создать отчет о выполненных проверках метрик.
  В директории будет создан файл metrics.tsv с записями о проверках.
* `getMetricsTimeout` - number(default: `20000`); таймаут на запрос получения рассчитанных метрик из команды браузера к воркеру плагина в мс.

Компонент принимает следующие технические опции:

* `ipbusBrokerRunDir`, `ipbusBrokerLogDir` - string; параметры брокера [ipbus](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/ipbus) шины. 
  Должны быть указаны одинаковые значения с компонентом [archon-renderer](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/archon-renderer).
  Для генерации значений параметров следует использовать функции `generateBrokerRunDir`, `generateBrokerLogDir` из пакета @yandex-int/ipbus.


## Конфигурация

В корневой директории проекта должен быть файл `.yproject`, содержимое которого представляет собой валидный JSON.
В поле `paths.metricsFetcher` корневого объекта должна быть указана строка с путём до файла конфигурации MetricsFetcher.
Пример файла `.yproject`:
```json
{
    "paths": {
      "metricsFetcher": "./.config/metrics-fetcher.js"
    }
}
```

Файл конфигурации MetricsFetcher может быть в формате JavaScript или JSON. В примере конфига для всех параметров указаны значения по
умолчанию; если значения не нужно поменять для сервиса, то опции указывать не нужно:

```js
module.exports = {
    logs: {
        // Секция для описания серверных логов (логов показа, blockstat, baobab).
        blockstat: {
            // Необходим ли данный лог для проверок счетчиков и/или метрик
            needed: true,
            // Cписок названий файлов с blockstat и baobab логами, за которыми следит плагин.
            // В именах файлов "{port}" заменяется на порт report-renderer'а.
            fileNames: ['current-report-renderer_blockstat-{port}'],
            // Имя поля, в которое нужно поместить blockstat/baobab для запроса к демону метрик.
            daemonRequestName: 'blockstat'
        },
        // Секция для описания клиентских логов (redir).
        redir: {
            // Необходим ли данный лог для проверок счетчиков и/или метрик
            needed: true,
            // Список названий файлов с redir-логами, за которыми следит плагин.
            // В именах файлов "{port}" заменяется на порт clickdaemon'а.
            fileNames: ['redir-{port}.log'],
            // Имя поля, в которое нужно поместить redir для запроса к демону метрик.
            daemonRequestName: 'redir'
        },
        reqans: {
            // Необходим ли данный лог для проверок счетчиков и/или метрик
            needed: false,
            // Имя поля, в которое нужно поместить reqans для запроса к демону метрик.
            // Например, для СЕРП это reqans, а для Картинок - imgreqans.
            daemonRequestName: 'reqans'
        }
    },

    // Список обязательных для записи в клиентском (redir) логе параметров.
    // Отсутствие этих параметров свидетельствует о невалидности записи, и данная запись не включается в пул сработавших счётчиков.
    clientCounterRequiredFields: ['path', 'vars']
};
```
