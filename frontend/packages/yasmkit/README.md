# YasmKit
Простая и мощная интеграция с [Yasm](https://yasm.yandex-team.ru/) (он же Голован/Golovan) для nodejs-приложений. Умеет собирать статистику, отправлять ее в yasm с помощью встроенного сервера stat-ручки и строить динамические панели с графиками.

## Ключевые возможности
- сбор и агрегация статистики
- встроенный сервер [unistat-ручки](https://wiki.yandex-team.ru/jandekspoisk/sepe/monitoring/stat-handle/) для отправки статистики в yasm
- встроенный сервер для формирования динамических панелей с графиками из yasm (конфигурация панелей задается и хранится прямо в коде приложения и может изменяться на лету)
- для использования не требуется (хотя крайне желательно) [знакомство с yasm](https://doc.yandex-team.ru/Search/golovan-quickstart/concepts/about.xml)

## Установка
`npm i -S yasmkit`

## Использование
```js
const yasmkit = require('yasmkit');
yasmkit.server.run(); // Запускаем сервер stat-ручки, с помощью которой голован будет получать наши данные
yasmkit.metrics.addMaxLine('longest_resp_time'); // Максимальное время ответа за какой-то временной интервал
yasmkit.metrics.addSummLine('req_total_count'); // Суммарное количество запросов за какой-то временной интервал
...
yasmkit.addEvent('req_total_count'); // Увеличиваем счетчик запросов на единицу. На итоговом графике будет отображено общее количество
за заданный временной интервал
yasmkit.addEvent('longest_resp_time', respTime); // Учитываем время ответа на текущий запрос. На графике будет максимально долгий
const stats = yasmkit.collectStats(); // Также вместо использования сервера можем самостоятельно получить данные для stat-ручки
```

### TL; DR
Не хочешь читать много непонятных букв ниже? Смотри простейший пример в директории `./testapp` в этом репозитори. Также можешь взглянуть на [yasmkit-http-profiler](https://github.yandex-team.ru/unikoid/yasmkit-http-profiler). Только не жалуйся потом, что что-нибудь работает не так, как ты предполагал.


### Основные понятия
При сборе метрик YasmKit оперирует тремя ключевыми понятиями - _метриками_,_событиями_ и _агрегациями_.

**Метрика** - это любой числовой показатель эффективности или работоспособности вашего приложения (напр., количество запросов, обработанных за единицу времени или максимальное время обработки запроса).
Визуально метрику можно представить в виде графика.

Значение метрики определяется **событиями**, происходящими в приложении.
Каждое событие порождает какое-то число, которое должно быть учтено при вычислении итогового значения метрики (то есть точки на графике).

Как именно будет учтено значение того или иного события определяется **методом агрегации**.
Например, может быть посчитана сумма всех событий или же взято значение максимального из них.

### Типы метрик
На текущий момент YasmKit поддерживает два типа метрик, обычные линии и гистограммы. Значения гистограмм представляют собой не одно число, а набор.
Все числа из набора распределяются по нескольким диапазонам, каждый из которых имеет свой вес - количество значений, попавших в диапазон.
Гистограммы не могут быть визуализированны сами по себе, зато можно считать по ним квантили и процентили, средние значения, сумму и количество элементов в гистограмме и прочее.

### Как статистика отправляется в yasm
Собранную статистику может забрать Yasm, что позволит хранить и автоматизировать ее. Для этого в YasmKit предусмотрен сервер [stat-ручки]((https://wiki.yandex-team.ru/jandekspoisk/sepe/monitoring/stat-handle/)), которую периодически (обычно раз в 5 секунд) будет опрашивать yasmagent для сбора статистики с вашего приложения. Чтобы включить стат-ручку достаточно запустить сервер.

Если ваше приложение живет в Qloud, вам также нужно включить в настройках компонента флаг "Unistat" и указать адрес ручки (`/unistat`) и порт, на котором слушает сервер (по-умолчанию 8081, может быть изменен).
Если же приложение не в Qloud, вам нужно попросить админов развернуть на ваших хостах yasmagent и настроить его на опрос stat-ручки.

### Как работает агрегация
В yasmkit предусмотренно 4 _уровня агрегации_. То есть перед попаданием на график ваши данные агрегируются сначала в приложении (1) (чтобы посчитать итоговое значение метрики за интервал от одного опроса ручки агентом до следующего), затем сам yasm-агент может взять сырое значение из ручки, либо разницу с предыдущим значением (2).
После этого выполняется агрегация по группе хостов, где запущены экземпляры вашего приложения (3). Именно такое значение отображается на Realtime-графике в yasm.
Кроме того, при хранении истории yasm также применяет агрегацию для пересчета значений за более крупные временные интервалы (4).
Агрегацию на все уровни агрегации можно задать по своему усмотрению (с учетом ограничений Yasm и здравого смысла) при добавлении метрики в YasmKit. [Подробнее по агрегацию в документации Yasm.](https://doc.yandex-team.ru/Search/golovan-quickstart/concepts/signal-aggregation.xml)

### Как смотреть графики
Чтобы не искать графики своих метрик в Yasm по тегам и не строить руками панели с ними, Yasmkit предлагает возможность построения
панелей динамически, прямо в ходе работы приложения. Можно создавать множество панелей с различными графиками, группировать несколько
метрик на одном графике, задавать функции (автохэндлеры) от метрик и т.д.
На графиках могут быть не только метрики вашего приложения, но и другие, что полезно для выявления корреляций и сравнительного анализа.

## API

### Управление сервером
- `yasmkit.server` - управление встроенным сервером stat-ручки и динамических панелей
    - `.run([options])` - запустить сервер. Опционально принимает объект с конфигурацией. Доступные параметры
        - `[options.port=8081]` - порт, на котором будет слушать сервер
    - `.shutdown()` - выключить сервер. Удаляет обработчики событий сервера, что дает возможность процессу успешно завершиться.

### Настройка метрик и добавление событий
- `yasmkit.metrics` - позволяет добавлять метрики, указывая их конфигурацию
    - `.addCustomLine(metricName, options)` - добавить метрику типа "линия" с ручным заданием параметров агрегации на всех уровнях.
    `metricName` - название метрики
        - `options.aggregation` - настройки агрегации для всех уровней
            - `options.aggregation.instance` - агрегация на уровне приложения (то есть за интервал между опросами ручки yasmagent'ом, обычно 5 секунд). Допустимые значения: `'summ'`, `'max'`, `'min'`, `'last'`, `'aver'`
            - `options.aggregation.agent` - агрегация, которую выполняет yasmagent при опросе ручки. Допустимые значения: `'absolute'` и `'delta'`.
            - `options.aggregation.group` - агрегация по группе и метагруппе хостов. Допустимые значения - `'aver'`, `'max'`, `'min'`, `'summ'`, `'summnone'`, `'last'`.
            - `options.aggregation.history`- агрегация по длинным временым интервалам для исторических данных. Допустимые значения: `'aver'`, `'max'`, `'min'`, `'summ'`.
        - `options.resetOnRead` - сбрасывать ли значение метрики, после того, как оно отправлено в yasm. Фактически настройка влияет на две вещи: 1. Будет ли для событий, сгенерированных после отправки агрегация считаться "с нуля" или же относительно значения за предыдущий интервал опроса; 2. Если за интервал между отправкой данных не произошло событий, будет ли отправлено значение за предыдущий интервал или же NO DATA.
    - `.addHistogram(metricName, [options])` - добавить гистограмму.
        - `options.bucketFactor=1.5` - коэффициент, по которому считаются границы бакетов. Например, для `1.5` границы будут такие: `[..., 1.5^-1, 1.5^0, 1.5^1, 1.5^2, ...] = [..., 0.66, 1, 1.5, 2.25, 3.375, ...]`. Все значения, попавшие в один бакет, будут объеденены. Например, значения `1.6` и `1.7` будут округлены до ближайшей левой границы (`1.5`) и будут переданы в Голован как два события со значением: `1.5`.
    - `.addMaxLine(metricName, [options])` - добавить метрику, значением которой будет максимальное значение из всех событий по всем инстансам за временной интервал
    - `.addMinLine(metricName, [options])` - добавить метрику, значением которой будет минимальное значение из всех событий по всем инстансам за временной интервал
    - `.addSummLine(metricName, [options])` - добавить метрику, значением которой будет суммарное значение всех событий по всем инстансам за временной интервал
- `yasmkit.addEvent(metricName, [event])` - добавить событие по метрике metricName. event - числовое значение события. Если event не указан (null или undefined) - логика зависит от выбранной агрегации на инстансе, как правило такое событие игнорируется.
- `yasmkit.server.onReadUnistat(cb)` - позволяет добавить обработчик на событие опроса стат-ручки yasm-агентом. Обработчик получает единственным параметром функцию `addEvent`, аналогичную `yasmkit.addEvent`. С ее помощью он может добавить события по каким-либо метрикам. Обработчик должен быть синхронной функцией, либо возвращать Promise. Агент получает ответ стат-ручки только по завершению всех добавленных обработчиков. Ошибки, возникающие при работе обработчиков - игнорируются.
- `yasmkit.collectStats()` - возвращает значения метрик в формате стат-ручки, также сбрасывает значения для метрик, которые это предусматривают. Можно использовать вместо встроенного в yasmkit сервера, если хочется реализовать ручку в своем приложении.


### Настройка панелей

- `yasmkit.server.addPanel(panelConfig)` - добавить динамическую панель. Панель будет доcтупна под адресу http://<ваше_приложение>:<порт>/panel?panelId=<id_панели>. Для доступа может понадобиться дырка до сети/машины, в которой запущено приложение на нужный порт. Формат конфига панели следующий:
    - `panelConfig.id` - id панели, по которому можно будет открыть ее. Строка.
    - `[panelConfig.charts=[]]` - список объектов с конфигурацией графиков, которые нужно разместить на панели.
  Метод возвращает объект с единственным методом - `addChart(chartConfig)`, принимающим конфигурацию панели, такую же как в `panelConfig.charts`. С его помощью можно добавлять графики на панель после ее создания.
  Метод `addChart`, в свою очередь, возвращает объект с методом `addSignal(signalConfig)`, принимающий конфигурацию сигнала и добавляющий его на график.

Конфигурация графика для `panelConfig.charts` и `addChart()` выглядит так:

- `chart.title` - заголовок (название) графика для отображения
- `[chart.signals=[]]` - список сигналов (линии), которые нужно отрисовывать на графике.
- `[chart.width=1]` - ширина графика (в ячейках сетки)
- `[chart.height=1]` - высота графика (в ячейках сетки)
- `[chart.col=0]` - положение графика на странице (колонка сетки)
- `[chart.row=0]` - положение графика на странице (ряд сетки)

Конфигурация сигнала для `chart.signals` и `addSignal()`:

- `signal.title` - заголовок (название) линии сигнала на графике
- `[signal.metric]` - название метрики из YasmKit, по которой будет построен график. Если не задано, должен быть задан параметр `signal.name`
- `[signal.name]` - название метрики из Yasm (включая sigopt-суффикс), по которой будет построен график. Нужно для того, чтобы строить графики по метрикам других приложений или по метрикам, которые собираются не с помощью YasmKit (например, метрики платформы).
- `[signal.host=yasmkit.config('hosts')]` - по какому хосту или группе/метагруппе хостов строить график.
- `[signal.tag=yasmkit.config('tag')]` - по какому тегу Yasm строить график.
- `[signal.func]` - строить график не по значению метрики, а по значению какой-либо [функции (автохендлера)](https://doc.yandex-team.ru/Search/golovan-quickstart/concepts/handlers.xml#auto) от нее. Если функция не принимает никаких аргументов, кроме названия метрики - `signal.func` может быть строкой с названием функции, иначе - списком, где первый элемент - название функции, а все остальные - аргументы, которые должны быть после названия метрики при вызове функции. Напр, `func: ['hcount', '10', '20']` - для расчета количества элементов гистограммы, попадающих в диапазон от 10 до 20.

### Глобальные настройки YasmKit
- `yasmkit.config(name, [value])` - позволяет задать или прочитать глобальные настройки yasmkit. Если задан value - значение настройки name выставляется в value. Всегда возвращает текущее значение настройки name. Список возможных настроек:
    - `hosts` {string} - группа/метагруппа хостов, используемая по-умолчанию для графиков на панелях. Если приложение живет в Qloud, yasmkit автоматом выставляет 'QLOUD'.
    - `tag` {string} - тег инстанса, используемый по-умолчанию для графиков на панелях. Если приложение живет в Qloud, yasmkit автоматом выставляет параметры данного компонента, исходя из переменных окружения.
    - `debug` {boolean} - если этот флаг выставлен, некорректная работа с API yasmkit может вызвать исключение, иначе выводится запись в stderr. Настоятельно рекомендуется включать эту настройку на этапе разработки и тестирования и выключать в продакшне.
    - `logVerbose` {boolean} - более подробное логгирование. Полезно для отладки самого yasmkit.
