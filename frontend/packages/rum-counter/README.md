# Код отправки RUM счетчиков

![](Logo-640.png)

Реализует сбор и отправку пользовательских и технических метрик,
необходимых для понимания работы страницы на устройствах пользователей. За основу взят счетчик СЕРПа, к нему добавлены метрики Морды.

Состоит из двух основных частей:
* инлайновый код (инициализация счетчика, добавление observer'ов)
* код во внешнем скрипте (сбор и отправка всех данных)

Т.к. счетчик должен уметь встраиваться в сервис с любой сборкой/окружением, то код написан на vanilla js
и разбит на отдельные файлы. Способ их встраивания зависит от самого сервиса.

[Slack чат для всех вопросов](https://yndx-all.slack.com/archives/C01FB7ABAD9)

[Документация](https://wiki.yandex-team.ru/velocity/rum/) по API и разметке страницы

## Миграция

[Важные заметки о миграции](doc/migration.md)

## Примеры запросов в YT и Clickhouse

[Clickhouse](doc/clickhouse-yql-examples.md)

[YT](doc/yql-examples.md)

## Файлы
### Инлайновый код
`src/inline/`
* `interface.js` **обязательный** Базовый код, где объявлены методы для использования до загрузки основного кода
* `longtask.js` **обязательный** Сохраняет время, когда был заблокирован основной поток js
* `io.js` *опциональный* Засекает время отрисовки основного элемента для серверного рендеринга (см. `Метрики, которые нужно отправлять явно`)
* **обязательно** Инициализация – выставление настроек и пробрасываемых параметров

### Внешний код
`src/bundle/`
* `send.js` *опциональный* Реализует отправку счетчика, совместим с форматом СЕРПа. **Обязательный** для проектов вне инфраструктуры СЕРПа
* ⚠️ `implementation.js` **обязательный** Основной код по сбору данных (должен выполняться **после(!)** Ya.Rum.init())
* `bem.js` *опциональный* Отправка статистики загрузки i-bem
* `ajax.js` *опциональный* Отправка статистики об AJAX-запросах, если они организованы как в web4/fiji
* `onload.js` *опциональный* Отправка статистики полной загрузки страницы, а также внешних ресурсов
* `retries.js` *опциональный* Отправка статистики ретраев, а также внешних ресурсов
* `image-goodness.js` *опциональный* Отправка метрик загрузки видимых картинок
* `scroll.js` *опциональный* Отправка метрик плавности скролла

## Метрики
За время начала работы берется `performance.timing.navigationStart`

### Пользовательские
<table><tbody>
<tr>
<td>Название</td><td>Описание</td><td>Как считается</td>
</tr>
<tr>
<td>Первая отрисовка<br/><i>first&nbsp;contentful&nbsp;paint</i></td>
<td>Сколько времени пользователь ждет от начала работы до того момента, когда появилось какое-то содержимое</td>
<td>В порядке убывания:<br/>
-&nbsp;<a href="https://w3c.github.io/paint-timing/">Paint Timing API</a><br/>
-&nbsp;chrome.loadTimes().firstPaintTime<br/>
-&nbsp;performance.timing.msFirstPaint<br/>
</td>
</tr>
<tr>
<td>Отрисовка основного элемента<br/><i>first&nbsp;meaningful&nbsp;paint</i></td>
<td>Сколько времени пользователь ждет от начала работы до того момента, когда отобразился основной элемент (поисковая стрелка, первая карточка/сниппет/картинка и т.п.)</td>
<td>Серверный рендеринг:<br/>
-&nbsp;<a href="https://www.w3.org/TR/intersection-observer/">Intersection Observer API</a><br/>
Клиентский рендеринг:<br/>
-&nbsp;вставка содержимого в DOM + requestAnimationFrame
</td>
</tr>
<tr>
<td>Время до интерактивности<br/><i>time&nbsp;to&nbsp;interactive</i></td>
<td>Сколько времени пользователь ждет от начала работы до того момента, когда можно взаимодействовать со страницей (кликаются кнопки и т.п.)</td>
<td>Если поддерживается <a href="https://w3c.github.io/longtasks/">Long Task API</a>:<br/>
-&nbsp;время после DOMContentLoaded и окончания последнего long task'а, после которого 3 секунды не было других long task'ов<br/>
</td>
</tr>
<tr>
<td>Задержка первого взаимодействия<br/><i>first&nbsp;input delay</i></td>
<td>Сколько времени тратится на обработку первого пользовательского события на странице</td>
<td>
Считается по <a href="https://web.dev/fid/">документации</a>
</td>
<tr>
<td>Largest Contentful Paint (LCP)</td>
<td>Время отрисовки наибольшего по площади элемента,
произошедшей до ухода страницы в фон или до закрытия страницы</td>
<td>
Считается по <a href="https://web.dev/lcp/">документации</a>
</td>
</tr>
<tr>
<td>Largest Loading Element Paint</td>
<td>Время отрисовки наибольшего по площади элемента, произошедшей до события `load`</td>
<td>
Считается по <a href="https://web.dev/lcp/">документации</a> LCP за исключением того,
что значение отправляется при событии `load`, дальнейшие отрисовки значения для этой метрики не имеют
</td>
</tr>
<tr>
<td>Cumulative Layout Shift (CLS)</td>
<td>Оценка суммарных сдвигов визуальных элементов (больше – хуже), считается по особенной формуле, зависящей от площади и дистанции сдвигов. Увеличивается при наличии сдвигов в интерфейсе, не вызванных пользовательским действием</td>
<td>
Считается по <a href="https://web.dev/cls/">документации</a>
</td>
</tr>
<tr>
<td>Element Timing</td>
<td>Метрика, позволяющая отследить, в какой момент отобразились картинки или элементы на странице, размеченные специальным атрибутом `elementtiming="name"`</td>
<td>
Считается по <a href="https://wicg.github.io/element-timing/">документации</a>
</td>
</tr>
</tbody></table>

### Загрузка и выполнение скриптов
<table><tbody>
<tr>
<td>Название</td><td>Описание</td><td>Как считается</td>
</tr>
<tr>
<td>Время domContentLoaded<br/><i>dom&nbsp;content&nbsp;loaded&nbsp;start</i></td>
<td>Событие domContentLoaded
</td>
<td>performance.timing.domContentLoadedEventStart - performance.timing.navigationStart
</td>
</tr>
<tr>
<td>Время инициализации фреймворка<br/><i>js&nbsp;framework&nbsp;inited</i></td>
<td>Зависит от сервиса и фреймворка</td>
<td>Отправляется самостоятельно с помощью Ya.Rum.sendTimeMark('3036')
</td>
</tr>
<tr>
<td>Суммарное время лагов<br/><i>long&nbsp;task&nbsp;sum</i></td>
<td>Сумма всех интервалов времени, когда интерфейс не реагирует на действия пользователя</td>
<td>Если поддерживается <a href="https://w3c.github.io/longtasks/">Long Task API</a>:<br/>
-&nbsp;суммарное время всех long task'ов
</td>
</tr>
</tbody></table>

### Браузерные
<table><tbody>
<tr>
<td>Название</td><td>Описание</td><td>Как считается</td>
</tr>
<tr>
<td>Время domLoading<br/><i>dom&nbsp;loading</i></td>
<td>Событие domLoading
</td>
<td>performance.timing.domLoading - performance.timing.navigationStart
</td>
</tr>
<tr>
<td>Время domInteractive<br/><i>dom&nbsp;interactive</i></td>
<td>Событие domInteractive
</td>
<td>performance.timing.domInteractive - performance.timing.navigationStart
</td>
</tr>
<tr>
<td>Полная загрузка документа<br/><i>full&nbsp;load</i></td>
<td>Событие window.onload
</td>
<td>(время window.onload) - performance.timing.navigationStart
</td>
</tr>
</tbody></table>

### Сетевые
<table><tbody>
<tr>
<td>Название</td><td>Описание</td><td>Как считается</td>
</tr>
<tr>
<td>Время ожидания<br/><i>wait</i></td>
<td>Время до отправки dns запроса
</td>
<td>performance.timing.domainLookupStart - performance.timing.navigationStart
</td>
</tr>
<tr>
<td>Время dns без кэширование<br/><i>dns&nbsp;no&nbsp;cache</i></td>
<td>Время dns запроса без нулевых значений
</td>
<td>performance.timing.domainLookupEnd - performance.timing.domainLookupStart
</td>
</tr>
<tr>
<td>Время tcp без keep alive<br/><i>tcp&nbsp;no&nbsp;ka</i></td>
<td>Время tcp запроса без нулевых значений
</td>
<td>performance.timing.connectEnd - performance.timing.connectStart
</td>
</tr>
<tr>
<td>Время ssl без keep alive<br/><i>ssl&nbsp;no&nbsp;ka</i></td>
<td>Время ssl запроса без нулевых значений
</td>
<td>performance.timing.connectEnd - performance.timing.secureConnectionStart
</td>
</tr>
<tr>
<td>Время первого байта<br/><i>ttfb</i></td>
<td>Время ответа сервера
</td>
<td>performance.timing.responseStart - performance.timing.connectEnd
</td>
</tr>
<tr>
<td>Время скачивания ответа<br/><i>html</i></td>
<td>Время скачивания ответа сервера
</td>
<td>performance.timing.responseEnd - performance.timing.responseStart
</td>
</tr>
</tbody></table>

### Информация о локации CDN

Информация о локации берётся из скрипта [nearest.js](https://yastatic.net/nearest.js)
и пишется во все счётчики в переменную `-cdn`. Чтобы получить эту информацию, нужно подключить
этот скрипт на проекте раньше, чем RUM.

### Учёт трафика

На каждую загрузку страницы RUM отправляет информацию о потреблённом трафике через счётчик `tech.perf.traffic`.

Счётчик отправляется раз в N миллисекунд (можно отключить опцией `periodicStatsIntervalMs: null`),
а также на событие `beforeunload`.

Интервал отправки можно конфигурировать опцией `periodicStatsIntervalMs`. По умолчанию `15000`.

Максимальное количество отправленных счётчиков можно конфигурировать опцией `maxTrafficCounters`. По умолчанию `250`.

При настройках по умолчанию информация отправляется примерно в течение часа.

### Учёт долгих операций (long task)

Долгие операции считаются по умолчанию для определения TTI. Дальнейшие операции могут быть посчитаны, если включена опция `longTaskMetric`.

Раз в какое-то время RUM отправляет информацию об операциях через счётчик `tech.perf.long-task`. Таймер отправки тот же самый, что и в счётчике трафика.

Максимальное количество отправленных счётчиков можно конфигурировать опцией `maxLongTaskCounters`. По умолчанию `10`.

### Метрики скролла

Есть два варианта метрики скролла: на js, который работает во всех браузерах, и из браузера (YaBrowser 20.2+). Первый хорошо учитывает продолжительные операции на js, второй лучше реагирует на обработчики событий и отрисовку страницы.

Общий счётчик включается опцией `scrollMetric`.
Браузерный счётчик включается через `scrollLatencyMetric`.

Оба счётчика работают примерно одинаково: считаются времена между событиями / затраченные на события, складываются в список, затем считается среднеквадратичное и отправляется в виде одного числа.
Первая метрика отправляется под именем `tech.perf.scroll`, вторая - `tech.perf.scroll.latency`.

Ограничений на количество отправок нет.

### Метрика "хороших" картинок

Для получения этих метрик нужно подключить файл `bundle/image-goodness.js`. Счётчик собирает со страницы
элементы img, элементы с атрибутом `data-rcid` или элементы с инлайновым стилем, где указан `background`.

На сервер отправляется информация о минимальном и максимальном временах загрузки картинок, попавших во вьюпорт
в момент `DOMContentLoaded`.

Есть ограничение на минимальный размер блока с изображением, лучше всего смотреть код.

## Расчет метрик
* [Агрегированные данные в YT](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/velocity/rum/1d)
* [Отчет (обновляется ежедневно, задержка ~1.5 суток)](https://stat.yandex-team.ru/-/CBa1f6TQtB)

## Дашборд
* [Стандартный отчет времени загрузки сервисов](https://stat.yandex-team.ru/Dashboard/Velocity/General), можно создать свой на его основе с нужными метриками
* [Время загрузки всех сервисов, KPI](https://stat.yandex-team.ru/Dashboard/Velocity/KPI)

## Встраивание в сервис
* добавить
    * через npm: `npm install --registry https://npm.yandex-team.ru --save @yandex-int/rum-counter`
    * через Bower: в `bower.json` зависимость `"counter": "git://github.yandex-team.ru/RUM/counter#version"`,
  например `"counter": "git://github.yandex-team.ru/RUM/counter#v0.0.1"`. Список версий можно
  [посмотреть здесь](https://github.yandex-team.ru/RUM/counter/releases).
* добавить инлайновый и внешний код в свой сервис (собранный код находится в папке `/dist`)
* пробросить параметры для инициализации счетчика

```javascript
Ya.Rum.init({
    beacon: true, // использовать beacon API или нет
    clck: 'https://yandex.ru/clck/click', // хост для отправки счетчика
    slots: ['12345,0,0', '54321,0,0'], // test-id's или другие идентификаторы выборок, в которые попал показ
    reqid: '11111.2222.333.44', // уникальный id показа

    forcePaintTimeSending: isPrerender, // всегда отправлять отрисовки (например, при пререндере или после переключения вкладок)

    sendClientUa: expFlags.enableExtraRum, // отправлять клиентский UA
    sendBeforeBemInited: expFlags.enableExtraRum, // отправлять before_bem-init
    sendUrlInResTiming: expFlags.enableExtraRum, // отправлять URL в Resource Timing
    sendAutoResTiming: expFlags.enableExtraRum, // автоматически отправлять Resource Timing для размеченных
    sendAutoElementTiming: expFlags.enableExtraRum, // автоматически отправлять Element Timing для размеченных
    sendFirstRaf: expFlags.enableExtraRum, // отправлять первый rAF в методе sendRaf
}, {
    'region': '213', // регион из геобазы
    'rum_id': 'ru.test', // имя сервиса, первым токеном должен идти домен,
    '-blocker': 1 // признак показа под блокировщиками рекламы; если нет блокировщика - можно не передавать
});
```

Имя сервиса должно быть в формате `ru.<service>.<pageName>[.<pageName>]`, где
* `<service>` - имя сервиса
* `<pageName>` - логические разделы страниц, может быть несколько уровней вложенности, например:
  * `ru.morda.plain`
  * `ru.realty.desktop.card.offer`

Тут важно, что если вы не хотите различать логические разделы, а хотите различать только страницы вашего сервиса, то
можно сделать `rum_id = ru.<service>` (без точки на конце). И прокидывать страницу через параметр `-page`
(как дополнительный параметр).

Пример такого подключения:
* [services.py](https://a.yandex-team.ru/svn/trunk/arcadia/velocity/trencher/data-collector/velocity_rum/services.py?rev=r9565598#L470)
* [код счетчика](https://a.yandex-team.ru/arcadia/quality/ab_testing/scripts/adminka/adminka/templates/adminka/base.html?rev=r9566548#L27)


⚠️ Проверьте, что вы проходите фильтры на счетчик. Если это не так, то вы не появитесь
в логах RUM в YT.  (однако значения счетчиков уже можно будет смотреть через СlickHouse. [Пример запроса](https://yql.yandex-team.ru/Operations/YqDCmMlwvR_GtyLB-JQfVrFPlIlaqjZZ0oczRbR2TdM=))
[Фильтр на счетчики](https://a.yandex-team.ru/svn/trunk/arcadia/velocity/trencher/data-collector/velocity_rum/data_handling/data_provider.py?rev=r9506344#L417) ⚠️

После этого нужно сделать PR с добавлением маски этой страницы в
[код построения отчетов](https://a.yandex-team.ru/arc/trunk/arcadia/velocity/trencher/data-collector/velocity_rum/services.py?rev=r7784692#L35)

Нужно сделать форк, сделать PR и попросить посмотреть или влить кого-то из [команды скорости](https://abc.yandex-team.ru/services/velocityandstability/)

*Важно* - там вы указываете фильтр на подстроку. Если в конце строки есть `.`, а в счетчике на странице имя не содержит нескольких слов (то есть в нем нет разделителя `.`), то эти записи не попадут в отчет. Лучше всего сразу делать имя составным, отделяя тачевую версию от десктопной суффиксом (`ru.example.touch` и `ru.example.desktop`)

### RUM и SPA

В RUM метрики привязываются к ID запроса (reqid). Некоторые метрики при этом считаются кумулятивно до определённого события
(переход в фон, выгрузка страницы).

В случае аяксовых навигаций между страницами нужно явным образом отправлять и финализировать эти метрики:

```js
Ya.Rum.sendTrafficData();
Ya.Rum.finalizeLayoutShiftScore();
Ya.Rum.finalizeLargestContentfulPaint();
```

#### Замер скорости отрисовки SPA-контента
```js
// Пользователь нажал на кнопку, которая открывает попап/делает SPA-переход. Приложение тут же начинает поход по сети за данными.
window.Ya.Rum.spa.makeSpaSubPage('main-feed'); // 'main-feed' - имя подстраницы для примера.
// Приложение завершает поход по сети за данными.
window.Ya.Rum.spa.finishDataLoading('main-feed');
// Приложениe начинает отрисовку полученных данных.
window.Ya.Rum.spa.startDataRendering('main-feed');
```
Подробнее в [`rum-counter/doc/spa-metric.md`](doc/spa-metric.md)

## RUM и Turboapp

В Turboapp не всегда доступны сервисные reqid и uid. Например, в случае полностью клиентского рендеринга без похода на сервер.

В этом случае нужно использовать специальные поля, которые передаются в JS-контекст приложения:

```
yandex.private.user.yandexuid
yandex.private.user.reqid
```

Также в Turboapp нужно отделить статистику от основного веб-сервиса, для этого нужно назначить страницам, которые открываются в приложении, отдельные поля `rum_id` и `-platform`. Пример:

```javascript
Ya.Rum.init({
    beacon: true, // использовать beacon API или нет
    clck: 'https://yandex.ru/clck/click', // хост для отправки счетчика
    slots: ['12345,0,0', '54321,0,0'], // test-id's или другие идентификаторы выборок, в которые попал показ
    reqid: someServerReqid || yandex.private.user.reqid
}, {
    'region': '213', // регион из геобазы
    'rum_id': 'ru.test.' + (isTurboApp ? 'turbo-app' : 'mobile'), // имя сервиса, первым токеном должен идти домен
    '-platform': isTurboApp ? 'turbo-app' : 'mobile', // платформа для rum.yandex-team.ru
    '-blocker': 1, // признак того, что показ под блокировщиками рекламы. Если нет блокировщика, то можно не передавать
    '-uid': isTurboApp && yandex.private.user.yandexuid
});
```

### Метрики, которые нужно отправлять явно
* <i>first&nbsp;meaningful&nbsp;paint</i>
Для серверного рендеринга нужно подключить инлайновый файл `io.js` и вызвать `Ya.Rum.observeDOMNode('2876', '.hero')`, где `.hero` - селектор для определения основного элемента страницы. Этот вызов можно поместить сразу после инициализации счетчика.
Для клиентского рендеринга нужно вызвать метод `Ya.Rum.sendHeroElement()` после добавления dom-ноды с основным содержимым
* <i>js&nbsp;framework&nbsp;inited</i>
Нужно вызвать метод `Ya.Rum.sendTimeMark('js_framework_inited')` после инициализации фреймворка. Для `i-bem` можно подключить файл `src/bundle/bem.js`

### Разметка блокировщиков рекламы
* **На сервере** см. пример `Ya.Rum.init` выше
* **На клиенте** `Ya.Rum.sendTimeMark('id', Ya.Rum.getTime(), false, {'-blocker'': 1 /* то, что вернула размечалка блокировщиков */})`


### Debug-режим
Для debug режима нужно подключить скрипт:

`import '@yandex-int/rum-counter/debug/blockstat.js';`

И перед инициализацией вызвать `Ya.Rum.debug()`;

См. использование `?rumdebug=1` в [примере](#примеры-pr).
[Посмотреть вживую](https://l7test.yandex.ru/?rumdebug=1) (открыть консоль)

### Если страница в iframe
Если ваша страница находится в `iframe`, то момент `navigationStart` для нее наступит примерно на 1-2 секунды позже, чем для родительской страницы. От этого же момента будет отсчитываться событие `first contentful paint`.

Если `iframe` скрыт и не был показан, то `first contentful paint` не будет считаться, в отличие от других метрик, например, `tti`.

Если `iframe` все же был показан, то `first contentful paint` примерно будет совпадать с временем, когда это случилось (за вычетом той самой разницы в 1-2 секунды во временах `navigationStart`).

Если вы все-таки хотите считать `fcp`, то
* нужно подписаться на какое-то событие о том, что отрисовка произошла. Событие `visibilityChange` для этого не подойдет, так как видимость iframe [совпадает](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API) с видимостью родительской страницы, независимо от того, скрыт он или нет.
* по этому событию отправляете кастомную метку через `Ya.Rum.sendTimeMark('iframe.fcp')`
* мы сделаем поддержку этой новой метки `iframe.fcp` в отчете Тренчера `customTimeMarks`

### Если нужно передать кастомный URL

```javascript
Ya.Rum.init({
    // …
}, {
    'rum_id': 'ru.test',
    '-platform': 'mobile',
    '-url': 'https://example.com'
});
```


### Если нужно писать события в отдельные таблицы

Подключаем модуль `bundle/send-custom-table` _после_ модуля `bundle/send`.

```js
require('../../src/bundle/send');
require('../../src/bundle/send-custom-table');
```

В конфигурации `RUM` указываем префикс таблицы:

```js
Ya.Rum.init({
    // …
    tablePrefix: 'market'
}, {
    //
});
```

Теперь события будут отправляться в отдельные таблицы в зависимости от `path.

> Например, событие с `path=690.2096.207` отправится в таблицу `market_rum_ti`.


### Готовые виджеты для стата (можно изменять параметры и использовать в графиках на stat)
* [KPI метрика для сервиса для указанной процентили](https://charts.yandex-team.ru/editor/ivan-karev/velocity/kpi?fieldName=p95&metric=first_contentful_paint&limit=4500&std=2550&text=4500ms&filter=portal,yaru)
* [Подробная информация по метрике](https://charts.yandex-team.ru/preview/wizard/ivan-karev/velocity/metric?metric=first_contentful_paint&service=portal:morda.geotouch&limit=4500)
* [Универсальный виджет для subpage](https://charts.yandex-team.ru/preview/wizard/ivan-karev/velocity/metric_subpage?metric_name=delta_api&page_id=ru.morda.zen&rum_id=_total_)

### Примеры дашбордов
* [Скорость разных страниц Морды](https://stat.yandex-team.ru/Dashboard/User/ivan-karev/morda-performance)
* [Время загрузки директа на сервисах](https://stat.yandex-team.ru/Dashboard/User/ivan-karev/direct-performance)

### Примеры PR
* [Админка](https://a.yandex-team.ru/arcadia/quality/ab_testing/scripts/adminka/adminka/templates/adminka/base.html?rev=r9566548#L20)
* [Турбо](https://github.yandex-team.ru/serp/turbo/pull/581)
* [Морда](https://github.yandex-team.ru/morda/main/pull/736). Есть поддержка `?rumdebug=1`
* [Дзен](https://github.yandex-team.ru/zen/code/pull/1694)

## Реалтаймовые данные
Логи, в которых есть дополнительные поля, попадают в реалтаймовый ClickHouse. Их можно смотреть в [YQL](doc/clickhouse-yql-examples) или в интерфейсе https://rum.yandex-team.ru/

⚠️ Данные в ClickHouse хранятся несколько недель, исторические можно посмотреть на стате или в YT.

### Что нужно изменить в отправке счетчика
Нужно добавить во второй параметр при инициализации те же поля, что и для клиентских ошибок, только с префиксом '-' в имени.
```javascript
Ya.Rum.init({
    // ...
}, {
    // ...
    '-project': 'test', // Название проекта
    '-page': 'index', // Страница сервиса, например: index, search, product
    /* Все, что ниже, является опциональным. Эти параметры можно не передавать, если дефолтные значения подходят */
    '-env': 'development', // !! Доступные значения: development, testing, prestable, production
    '-platform': 'desktop', // !! Доступные значения: desktop, touch, pad, app, tv, tvapp
    '-version': '1.1', // Версия [статики] вашего приложения
    experiments: ['first_exp', 'second_exp'].join(';'), // Имена экспериментальных выборок через ;
});
```
[Пример1](https://gitlab.yandex-team.ru/morda/main/blob/dev/tmpl/common/blocks/timing/timing.view.js#L88)

[Пример2](https://gitlab.yandex-team.ru/serp/chat/pull/3387/files#diff-8b5c74f40d25e64537ec401342c4235aR44)

## Пример использования
* Исходный код: `example/src/`
* Сборка примера: `npm run build-example`
* Собранный пример: `example/build/`

**NB:** Вызовы счётчиков для замера времени выполнения кода подставляются в результирующий файл бандла во время сборки (см. `banner` и `footer` в `rollup.config.js`)

## Тестирование

У RUM есть два вида тестов: unit и e2e. Они расположены в директории test

Для запуска в пулл-реквестах используется [Трендбокс](https://gitlab.yandex-team.ru/search-interfaces/trendbox-ci/blob/master/README.md)

*Важно* - В данный момент e2e тесты не запускаются в пулл-реквестах. Нужно обязательно вызывать тесты руками перед коммитом `npm run test`

Для тестирования RUM в Sandbox требуется специально собранный контейнер.
Тип ресурса для этого контейнера – [TRENDBOX_CI_LXC_IMAGE_BETA](https://sandbox.yandex-team.ru/resources?type=TRENDBOX_CI_LXC_IMAGE_BETA&page=1&pageCapacity=20&attrs=%7B"rum_lxc_image"%3A"1"%7D)
с атрибутом `rum_lxc_image=1`
