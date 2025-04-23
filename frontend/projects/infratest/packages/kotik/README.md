# Kotik

[![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/kotik)](https://oko.yandex-team.ru/pkg/@yandex-int/kotik)

Kotik - это сервер на основе [express](http://expressjs.com/).
Он использует ту же идею middleware(req, res, next), что и express.
Middleware от express подходят для kotik.
Основные отличия:

* большое количество yandex-специфичных и dev-специфичных middleware в составе
* заточен под работу с [archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html)
* многопроцессорный, есть возможность запуска большого количества worker'ов

Kotik пришёл на замену [templar](https://doc.yandex-team.ru/si-infra/local_devserver/templar.html) без серповых костылей и с поддержкой фич `app_host+report-renderer`.


## Мотивация


Темплар создавался как инструмент для локальной разработки Серпа (читай `web4`).
С тех пор появились новые проекты и, как результат, новые хотелки, которые сложно реализовать в архитектуре, изначально рассчитанной только на Серп.
Это привело к появлению множества костылей как на стороне проектов, так и в самом Темпларе.

Финальным аккордом можно считать появление проектов на стеке `http_adapter+app_host+report-renderer`: Услуги, Здоровье и других.

Им не нужно патчить объект `reqdata` (у них его нет), реализовывать пресёрч (у них может быть хоть 18 фаз шаблонизации), и так далее.
Для таких проектов Темплар был отличной иллюстрацией цитаты:
> You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.


## Устройство


Котик обрабатывает роуты, которые описаны в [конфигурационном файле](#format-konfiguratsionnogo-faila), так, как это описано в конфиге.

Чтобы опознать роут, котик использует [`matcher`](#matcher). Для матчинга запроса в большинстве случаев используется `pathname`, но могут быть использованы любые другие доступные признаки.

Чтобы обработать запрос к роуту, котик выполняет [`handler`](#handler). Для обработки запроса используются [мидлвары](#middlewares) или наборы мидлваров - [пресеты](#preset). Можно делать что угодно: отдавать файлы с файловой системы, проксировать запросы на бэкэнд с кешированием и без, с патчингом данных и без, генерировать ответ в мидлваре. Есть некоторое количество [готовых мидлваров](#vstroennye-midlvary) и [готовых пресетов](#gotovye-presety).

Мидлвары могут обмениваться данными между собой через [контекст котика](#peredacha-dannyh-mezhdu-midlvarami) и с внешними процессами через [ipbus](https://doc.yandex-team.ru/si-infra/common_packages/ipbus.html).


## Рецепты


### Минимальный пример

#### 1. Установите необходимые пакеты

Котик оформлен в виде компонента [archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html),
поэтому для использования необходимо включить его в состав archon-команды.

Для большинства случаев подойдут готовые команды из пакета [archon-devserver-command](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-devserver-command.html) или [archon-renderer-devserver-command](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/archon-renderer-devserver-command.html).

```bash
$ npm i --save-dev @yandex-int/archon --registry https://npm.yandex-team.ru
$ npm i --save-dev @yandex-int/archon-devserver-command --registry https://npm.yandex-team.ru
```

#### 2. Создайте конфиг проекта

Конфиг проекта - это файл с именем `.yproject` в формате `json`. Его нужно расположить в корне вашего проекта.

В конфиге проекта в поле `paths.archon` укажите путь от корня проекта до директории, в которой будет располагаться конфиг archon.

```json
{
    "paths": {
        "archon": "./.config/archon"
    }
}
```

#### 3. Настройте archon

Конфиг archon расположите в директории, которая указана в `.yproject`. Сам файл должен быть назван `config.json`.
Для примера выше конфиг будет расположен по пути `.config/archon/config.json`.

В конфиге archon укажите список подключаемых команд. Подключение команды для запуска девсервера `archon-devserver-command` будет выглядеть так:

```json
{
    "commands": [
        "@yandex-int/archon-devserver-command/commands/just-kotik"
    ]
}
```
#### 4. Настройте kotik

Конфиг kotik расположите по пути `.config/kotik/config.js` (путь [не настраивается](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/kotik/constants/config-location.js?rev=r6863250#L5)).

Чтобы kotik начал обрабатывать роуты, нужно настроить их в конфиге. В данном примере на все запросы будет возвращаться `Hello, World!`:

```javascript
function helloMiddleware(req, res, next) {
  res.writeHead(200);
  return res.end('Hello, World!');
}

module.exports = {
  routes: [
    {
      matcher: (req) => true,
      handler: [
        { name: 'hello', fn: helloMiddleware }
      ]
    }
  ]
};
```

Результат проделанных шагов - [этот тестовый проект](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-devserver-command/src/__fixtures__/tutorial-project).

Убедитесь в работоспособности собранной конфигурации:

1. Запустите ваш девсервер командой `npx archon kotik`.
2. Откройте в браузере урл девсервера, который будет указан в логах консоли, например, `Kotik слушает на http://localhost:3333`.

По аналогии настройте необходимые вашему проекту роуты. В качестве примеров используйте:

- [пример конфига для тестов](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-renderer-devserver-command/test/fixtures/test-project/.config/kotik/config.js),
- [пример конфига web4](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/.config/kotik/config.js),
- конфиги котика из знакомых вам проектов.

Полное описание формата конфига kotik вы можете найти ниже в разделе [Формат конфигурационного файла](#format-konfiguratsionnogo-faila).


### Использование kotik в качестве кеширующего сервера

Зачастую в тестах нужно эмулировать сторонний бэкенд, имеющий http-интерфейс.
Это нужно, например, чтобы гарантировать время ответа сервера или неизменность ответа – ведь сервер может изменить свой ответ и тогда наши тесты упадут.
Одним из подходов для такой эмуляции является кеширующий сервер: при написании или обновлении теста мы запустим кеширующий сервер в режиме записи, когда он запроксирует запросы к реальному бэкенду, а ответы сохранит на файловой системе.
После этого можно запускать кеширующий сервер в режиме чтения, когда на каждый запрос он будет отвечать сохранённым ответом, а запросов к реальному бэкенду не будет.

Например, этот механизм используют [hermione](https://doc.yandex-team.ru/si-infra/hermione/hermione.html)-тесты верстки на дампах.

Пример настройки можно посмотреть в [фикстурах archon-devserver-command](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-devserver-command/src/__fixtures__/caching-example), а примеры запуска и использования такого сервера – в [тестах archon-devserver-command](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-devserver-command/src/__func__/index.test.ts?rev=04c077a1c69e07e2bb610ea72cdb7f37b5ff56da#L101).

Для того, чтобы использовать котик в качестве кеширующего прокси, нужно:

- подключить пресет [`regular-frontend-dynamic`/`apphost-frontend-dynamic`](#gotovye-presety) из kotik,
- добавить в начало мидлвар, который будет [устанавливать имя файла с кешом](#1-opredelenie-puti-k-failu-dampa),
- настроить адрес проксирования для запроса в [контексте роута](#context).

Запускать тесты с котиком можно несколькими способами:

* запускать и тесты и котик при помощи archon (предпочитаемый способ, при этом аргумент для выбора режима работы kotik доступен из коробки)
* запускать archon из кода тестов при помощи [child_process.exec](https://nodejs.org/docs/latest-v12.x/api/child_process.html#child_process_child_process_exec_command_options_callback)
* запускать archon из кода тестов при помощи ComponentManager, пример можно посмотреть в [тестах archon-devserver-command](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-devserver-command/src/__func__/index.test.ts?rev=04c077a1c69e07e2bb610ea72cdb7f37b5ff56da#L56)

Тогда тестирование может быть устроено таким образом:

* при первом запуске или изменении теста запускаем kotik в режиме write (опция --)

#### Устройство кеширования ручек

Механизм кеширования состоит из нескольких фаз, каждая из которых реализуется собственным мидлваром.
Мидлвары для каждой из этих фаз есть среди встроенных мидлваров котика, кроме мидлвара для определения имени файла дампа.
Этот мидлвар каждому сервису нужно определить самому. Как это сделать, описано в разделе [Определение пути к файлу дампа](#1-opredelenie-puti-k-failu-dampa).

Из встроенных мидлваров собраны готовые к подключению на проекте [пресеты](#preset). В большинстве случаев будет достаточно использовать их:

- для AppHost-ручек - [apphost-frontend-dynamic](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-renderer-devserver-command/index.js?rev=675d39eb22623d10cc04674faca626b952116926#L44),
- для обычных ручек - [regular-frontend-dynamic](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-renderer-devserver-command/index.js?rev=675d39eb22623d10cc04674faca626b952116926#L45).

При необходимости можно собрать свою цепочку мидлваров для обработки роута с кешированием. Чтобы кеширование заработало, в его обработке должны присутствовать следующие мидлвары строго в таком порядке друг относительно друга:

##### 1. Определение пути к файлу дампа

Для определения пути к файлу дампа требуется определить папку для сохранения дампа и имя файла, то есть добавить два мидлвара в цепочку обработки запроса.

Первый мидлвар - для определения пути к папке. Для этого подойдет коробочный мидлвар - `cachePath`.
Подробности о его работе можно узнать в [его описании](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#cachepath).
Если вам не подходит стандартный мидлвар, или вы по каким-то причинам не используете плагин `url-decorator`, то `cachePath` нужно выставить самостоятельно по аналогии с `cacheFilename` (см. ниже).

Второй мидлвар - для определения имени файла. Коробочного мидлвара не существует. Для каждого проекта требуется написать свой мидлвар,
который будет выставлять имя файла в контекст запроса котика в поле `cacheFilename`. [Как работать с контекстом](#peredacha-dannykh-mezhdu-midlvarami).

Например:
```javascript
const {presets} = require('@yandex-int/archon-renderer-devserver-command');
module.exports = {
  routes: [
    {
      matcher: (req) => req.kotik.parsedURL.pathname.startsWith('/uslugi'),
      handler: presets['apphost-frontend-dynamic']
        .addFirst({
          name: 'addCacheFilename',
          fn: (req, res, next) => {
            req.kotik.ctx.set('cacheFilename', `${req.kotik.parsedURL.searchParams.toString()}.json.gz`);
            next();
          }
        })
    }
  ]
};
```

При вычислении имени файла учитывайте следующие обстоятельства:

* котик **не** добавит расширение файла автомагически;
* имя файла должно укладываться в 255 байт (требование большинства современных ОС), котик посчитает обратное ошибкой;
* приводите имя к одному регистру – HFS+ (файловая система macOS) по умолчанию не case-sensitive;
* если вы хотите сохранить человекочитаемые имена файла и при этом удобство работы с ними – рекомендуем транслитерировать кириллицу и заменять пробелы;
* изучите любые другие ограничения релевантных вам ОС, [например](https://ru.wikipedia.org/wiki/Сравнение_файловых_систем#Ограничения);
* в любой непонятной ситуации – хешируйте вычисленную строку.

##### 2. Чтение данных с файловой системы

Мидлвар для чтения данных с файловой системы должен располагаться перед остальными мидлварами для работы с дампами,
чтобы можно было реализовать смешанный режим работы с дампами - `create`.

Чтение дампов реализуют мидлвары [`cacheReaderApphost`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#cachereaderapphost)
и [`cacheReaderRegular`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#cachereaderregular).

##### 3. Получение данных от бэкэнда

Для обработки запросов без использования дампа или для его записи, требуется поход в бэкэнд.

Для этой цели реализованы миддлвары [`getDataAppHost`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#getdataapphost)
и [`getDataRegular`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#getdataregular).

##### 4. Запись данных от бэкэнда на файловую систему

Сохранение данных, полученных от бэкэнда, реализуется мидлварами [`cacheWriterAppHost`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#cachewriterapphost)
и [`cacheWriterRegular`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#cachewriterregular).

##### 5. Отправка результата обработки данных с файловой системы или от бэкэнда

После получения данных из дампа или от бэкэнда в зависимости от типа ручки их может потребоваться обработать (например, отрендерить шаблоны или пропатчить).
Если обработка требуется, она должна производиться в мидлваре, стоящем в цепочке после записи данных на файловую систему и до отправки результата.

Для отправки результата реализованы мидлвары [`flushResponseAppHost`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#flushresponseapphost)
и [`flushResponseRegular`](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#flushresponseregular).

#### Отладка запроса за данными

При получении данных от бэкэнда встроенные миддлвары выводят в консоль на уровне логгирования `info` урл запроса и его `ReqId` в строке вида `Resolved request "...", reqid "..." [... ms]`.

Если проблема воспроизводится стабильно, то можно взять урл и поделать с ним запросы, добавляя [отладочные параметры AppHost](https://docs.yandex-team.ru/apphost/pages/cgi).

Если же проблему сложно воспроизвести, то, используя `ReqId`, можно поисследовать сделанный котиком запрос при помощи [SeTrace](https://wiki.yandex-team.ru/setrace/). Обратите внимание на ошибки и таймайты при обработке источников.


### Патчинг данных или ответа

В зависимости от задачи можно патчить данные или отрендеренный ответ (актуально, если в обработке ручки есть рендеринг).

Патчинг данных может быть полезен для "осовременивания" сохраненного дампа или любой другой подмены значений в данных до записи в дамп или после.
Например, патчинг используется для подмены reqId в данных на свежий для того, чтобы работали проверки счетчиков и метрик (реализован во встроенных мидлварах [replaceReqIdAppHost](#replacereqidapphost) и [replaceReqIdRegular](#replacereqidregular)).
Или для подмены имени коллбэка для ручек с JSONP ответом (реализован во встроенных мидлварах [addJsonpCallbackAppHost](#addjsonpcallbackapphost) и [addJsonpCallbackRegular](#addjsonpcallbackregular)). 

Чтобы пропатчить данные, нужно встроиться в цепочку мидлваров после получения данных с файловой системы ([cacheReaderAppHost](#cachereaderapphost), [cacheReaderRegular](#cachereaderregular)) или от бэкэнда ([getDataAppHost](#getdataapphost), [getDataRegular](#getdataregular)) и до рендеринга ([render](#render)) или отдачи ответа ([flushResponseAppHost](#flushresponseapphost), [flushResponseRegular](#flushresponseregular)). Местоположение полученных данных можно узнать в документации к мидлварам, которые были использованы.

Патчинг отрендеренного ответа может быть нужен при необходимости подменить что-то уже после рендеринга, хотя большинство задач решаются патчингом данных.

Чтобы пропатчить результат рендеринга, нужно встроиться в цепочку мидлваров после рендеринга ([render](#render)) и до отдачи ответа ([flushResponseAppHost](#flushresponseapphost), [flushResponseRegular](#flushresponseregular)).


### Установка/чтение режима работы с дампами

Котик позволяет изменять режим работы с дампами - `cacheMode` - во время работы девсервера через шину межпроцессного взаимодействия [ipbus](https://doc.yandex-team.ru/si-infra/common_packages/ipbus.html).

Чтобы узнать текущий режим работы с дампами внутри мидлвара, достаточно обратиться к `req.kotik.setup.params.cacheMode`. Во всех остальных случаях нужно подписаться на топик `dumps-cache-mode.get.result` и послать по шине сообщение `dumps-cache-mode.get`.

Чтобы переключить режим работы с дампами, нужно установить новое значение `cacheMode`. Для этого нужно подписаться на топик `dumps-cache-mode.set.result` и послать по шине сообщение `dumps-cache-mode.set` с новым значением.

{% note warning "Внимание!" %}

Мы не рекомендуем изменять `cacheMode` в мидлварах, так как это может приводить к непредсказуемым последствиям: когда часть кода обработки запроса отработает с одним значением `cacheMode`, а другая часть – с новым значением.

{% endnote %}

Пример использования:

```javascript
const pTimeout = require('p-timeout');
const { Bus } = require('@yandex-int/ipbus');

const TIMEOUT = 1000;

async function waitIpbusEvent(bus, eventName) {
    return new Promise(async function(resolve, reject) {
        try {
            await bus.subscribe(eventName, result => resolve(result));
        } catch (e) {
            reject(e);
        }
    });
}

async function getKotikCacheMode() {
    const bus = await Bus.create();

    try {
        const getCacheMode = waitIpbusEvent(bus, 'dumps-cache-mode.get.result');

        bus.send('dumps-cache-mode.get', Buffer.from(''));

        const errMsg = `failed to get cache mode for ${TIMEOUT} ms`;
        const cacheMode = await pTimeout(getCacheMode, TIMEOUT, errMsg);

        return cacheMode;
    } finally {
        await bus.close();
    }
}

async function setKotikCacheMode(newCacheMode) {
    const bus = await Bus.create();

    try {
        const setCacheMode = waitIpbusEvent(bus, 'dumps-cache-mode.set.result');

        bus.send('dumps-cache-mode.set', Buffer.from(newCacheMode));

        const errMsg = `failed to set cache mode "${newCacheMode}"`;
        const cacheMode = await pTimeout(setCacheMode, TIMEOUT, `${errMsg} for ${TIMEOUT} ms`);

        if (cacheMode.toString() !== newCacheMode) {
            throw new Error(errMsg);
        }
    } finally {
        await bus.close();
    }
}
```


### Очистка списка загруженных в report-renderer шаблонов

Очистка списка загруженных в report-renderer шаблонов - часть механизма пересборки шаблонов на лету.
После пересборки необходимо очистить список загруженных шаблонов, чтобы в report-renderer начали загружаться обновленные шаблоны.

За очистку отвечает поле контекста котика `clearLoadedTemplates`, которое обрабатывается в мидлваре [render](#render). [Как работать с контекстом](#peredacha-dannykh-mezhdu-midlvarami).

Пример задания значения:
```javascript
(req, res, next) => {
    req.kotik.ctx.set('clearLoadedTemplates', true);
    next();
}
```


## Технические подробности


### Формат конфигурационного файла

#### routes

Обязательное поле.
Содержит определения роутов.
Для поддержки динамической композиции роутов и обработчиков в качестве routes может быть указана функция (допускается асинхронная), принимающая опции kotik и kotik-логгер и возвращающая определения роутов.

```javascript
routes: [
    {
        // matcher: () => {}
    }
]
```

Для описания роута указываются матчер, обработчик и контекст запроса.

##### matcher

Обязательное поле. Функция проверяет, что именно этот роут нужно применить.

```javascript
matcher: (req) => {
    return req.kotik.parsedURL.pathname.startsWith('/uslugi');
};
```

##### handler

Список обработчиков (мидлваров), которые по очереди обрабатывают пользовательский запрос.
Подробнее про формат и использование мидлваров читайте в разделе [Middlewares](#middlewares).

```javascript
{
    matcher: (req) => req.kotik.parsedURL.pathname.startsWith('/awesome'),
    handler: [
        {name: 'my-awesome-middleware-1', fn: (req, res, next) => {...}},
        {name: 'my-awesome-middleware-2', fn: (req, res, next) => {...}}
    ]
}
```

Для поддержки динамической композиции обработчиков в качестве `handler` может быть указана функция (допускается асинхронная), принимающая опции kotik и kotik-логгер и возвращающая список обработчиков.

```javascript
{
    matcher: (req) => req.kotik.parsedURL.pathname.startsWith('/awesome'),
    handler: (kotikOptions, kotikLogger) => {
        return [
            {name: 'my-awesome-middleware-1', fn: (req, res, next) => {...}},
            {name: 'my-awesome-middleware-2', fn: (req, res, next) => {...}}
        ];
    }
}
```

Также в качестве `handler` можно использовать пресет – определенную цепочку мидлваров. Подробнее читайте в разделе [Preset](#preset).

```javascript
const {presets} = require('@yandex-int/archon-renderer-devserver-command');

{
    matcher: (req) => req.kotik.parsedURL.pathname.startsWith('/awesome'),
    handler: presets['apphost-frontend-dynamic']
}
```

##### context

###### context.source

Обязательное поле – url источника данных. Должен представлять собой валидный [WHATWG URL](https://nodejs.org/dist/v8.6.0/docs/api/url.html#url_the_whatwg_url_api).
```javascript
context: {
    source: {
        hostname: 'hamster.yandex.ru',
        protocol: 'https',
        searchParams: {renderer_export: 'binary'},
        headers: {'HEADER-NAME': 'value'},
    }
}
```

- `pathname` и `protocol` будут взяты из пользовательского запроса, если не указаны.
- `headers` добавят/заменят заголовки к запросу.
- `searchParams` будут добавлены к запросу. В `searchParams` указываются параметры запроса, необходимые **для получения данных, а не результата шаблонизации**. Kotik трактует этот параметр как аргумент для конструктора [URLSearchParams](https://nodejs.org/dist/latest/docs/api/url.html#url_class_urlsearchparams). Примеры отдельных параметров для `searchParams`:

  - `renderer_export: 'binary'` — включает экспорт данных для шаблонизации в формате AppHost;
  - `renderer_render_on_export: '1'` — указывает выполнять шаблон перед экспортом. Полезно в случаях, когда в одном из шаблонов модифицируется контекст.

**Важно:** в отличие от Темплара, Котик не предоставляет никаких значений по умолчанию.

#### localRendererSourceRewrites

Котик умеет перенаправлять запросы из графа в локально запущенный report-renderer.

Для этого нужно указать имя узла с report-renderer и тайм-аут на запрос, оба поля являются обязательными. Можно указать несколько узлов, например:

```javascript
localRendererSourceRewrites: [
    {
        name: 'TEMPLATE_ROUTER',
        timeout: 5000
    },
    {
        name: 'TEMPLATE_RENDER',
        timeout: 5000
    }
]
```

Запрос из графа пройдёт через [Tunneler](https://wiki.yandex-team.ru/users/unikoid/tunneler/) в report-renderer, запущенный локально.

Также вам может понадобиться донастройка графа: [документация на вики](https://wiki.yandex-team.ru/search-interfaces/infra/dev-at-apphost/#vazhnopronastrojjkugrafa).

#### loggerHandlers

Для перехвата логируемых внутри Котика событий (например для сбора статистики) через опцию `loggerHandlers` можно добавить свои обработчики:

```javascript
loggerHandlers: {
    customHandler: require.resolve('path/to/custom-handler')
}
```

Сам обработчик должен быть реализован как [log4js appender](https://github.com/log4js-node/log4js-node/blob/master/docs/writing-appenders.md).

Минимальный пример:

```javascript
exports.configure = function() {
    return function(loggingEvent) {
        console.log(loggingEvent);
        /**
         * LoggingEvent {
         *   startTime: 2020-06-10T07:21:43.789Z,
         *   categoryName: 'worker #1 (36518)',
         *   data: [ 'Kotik listen \u001b[34m\u001b[4mhttp://localhost:3333\u001b[24m\u001b[39m' ],
         *   level: Level { level: 20000, levelStr: 'INFO', colour: 'green' },
         *   context: {},
         *   pid: 36518
         * }
         */
    };
};
```


### Middlewares

#### Декларация мидлваров

Для обработки роута мидлваром, его нужно задекларировать в конфигурационном файле в поле `handler` в следующем формате:

* `name [required] [string]` — название мидлвара
* `fn [required] [function]` — обработчик

Пример:
```javascript
handler: [
    {name: 'my-awesome-middleware-1', fn: (req, res, next) => {...}},
    {name: 'my-awesome-middleware-2', fn: (req, res, next) => {...}}
]
```

#### Работа с данными из графа

Для работы с данными из графа существует следующее API:

* `addItem(value, type)` — добавит объект `value` с типом `type` в ответы `REPORT_RENDERER` всех источников
* `addJsonItem(jsonValue, type)` — делает то же самое, что и `addItem`, но первым аргументом принимает строку JSON. jsonValue будет преобразован при помощи `JSON.parse`
* `getItems(type)` — вернёт все элементы с типом `type` из всех ответов всех источников.
* `getOnlyItem(type)` — вернёт единственный элемент с типом `type` (бросит ошибку, если найдет ответов с типом `type` больше одного)
* `findFirstItem(type)` — вернёт первый найденный элемент с типом `type`
* `findLastItem(type)` — вернёт последний найденный элемент с типом `type`
* `addSourceData(name, data)` — добавит новый источник с именем `name` и данными `data` в дамп ответа AppHost'а
* `getSourcesData(name)` — вернёт все данные источников с именем `name` или, если `name` не указан, то все данные всех источников. Результат представлен массивом объектов, которые содержат поля имя `name` и данные `data`
* `sources` — вернёт все источники

Пример:
```javascript
(req, res, next) => {
    const request = req.kotik.ctx.findLastItem('http_request') || {};
    console.log(`request url: ${req.uri}`);
}
```

#### Передача данных между мидлварами

Для передачи данных из одного мидлвара в другой необходимо использовать контекст `req.kotik.ctx`, который имеет следующее API:

* `set(name, value)` — добавляет в контекст поле с названием `name` и значением `value`
* `get(name)` — получить из контекста значение
* `has(name)` — проверить установлено ли уже значения

Данные, установленные через `set`, не записываются в дампы.

Пример:
```javascript
[
    (req, res, next) => {
        req.kotik.ctx.set('msg', 'hello');

        next();
    },
    (req, res, next) => {
        if (req.kotik.ctx.has('msg')) {
            const msg = req.kotik.ctx.get('msg');
            return res.send(msg);
        } else {
            next();
        }
    }
]
```

#### Передача данных из мидлвара в другой процесс

Для передачи данных из мидлвара в другой процесс (например, в плагин hermione) необходимо использовать функцию `req.kotik.sendMsg`, которая отправляет сообщения по шине межпроцессного взаимодействия [ipbus](https://doc.yandex-team.ru/si-infra/common_packages/ipbus.html).

Пример мидлвара:
```javascript
(req, res, next) => {
    req.kotik.sendMsg('myTopic', Buffer.from('hello world'));
    next();
}
```

Пример с получением данных в hermione-плагине можно посмотреть [тут](https://doc.yandex-team.ru/si-infra/common_packages/ipbus.html#primer).

#### Отладка мидлваров

Если вы обнаружили, что установленное вами значение в контексте (`req.kotik.ctx`) изменилось на совершенно другое, это означает, что какой-то из мидлваров, выполняющийся после вашего, переписал его. Чтобы раздебажить такой кейс не обязательно бегать по коду всех мидлваров, достаточно запустить Котика в режиме `verbose`.

В этом случае в лог будет выведена информация о каждом установленном поле в контексте, а также в каком мидлваре это было сделано.

Пример:
```javascript
{name: 'my-middleware', fn: (req, res, next) => {
    req.kotik.ctx.set('foo', 'bar');
    req.kotik.ctx.set('foo', 'qux');
}}
```

Лог:
```
"my-middleware" middleware: set the field "foo" to "bar", previous value "undefined"
"my-middleware" middleware: set the field "foo" to "qux", previous value "bar"
```

Возможность инспектировать миддлвары будет реализована в рамках задачи [FEI-22659: kotik: возможность инспектировать миддлвары](https://st.yandex-team.ru/FEI-22659).

#### Встроенные мидлвары

Встроенные мидлвары закреплены в отдельном неймспейсе `middlewares`:

```javascript
// например, serveStatic middleware:
const {middlewares: {serveStatic}} = require('@yandex-int/kotik');

// где-то в конфиге котика:
handler: [
    {name: 'my-static', fn: serveStatic(serveStaticOptions)}
]
```

##### addJsonpCallbackAppHost
Middleware для преобразования данных AppHost-backend ответа в jsonp-callback. Имя callback добавляется или заменяется по необходимости.

##### addJsonpCallbackRegular
Middleware для преобразования данных не-AppHost-backend ответа в jsonp-callback. Имя callback добавляется или заменяется по необходимости.

##### bodyParser
Middleware парсинга body запросов (кроме multipart/form-data). Добавляет `req.body`.

[Подробнее в документации](https://www.npmjs.com/package/body-parser)

##### bodyUnifier
Middleware унификации данных от bodyParser и connectBusboy. Добавляет `req.unifiedBody` - объект с методами:

* `isEmpty()` - boolean. Есть ли у запроса body.
* `stringify()` - string. Строковое стабильное представление body. Может быть полезно при генерации имени дампа: разложить в разные дампы ответы на запросы с разным контентом.
* `getBody()` - string, Buffer или [FormData](https://www.npmjs.com/package/form-data). Body для запроса в backend (прежде всего для middleware `getData`).
* `getHeaders()` - object. Дополнительные заголовки для правильного запроса multipart/form-data в backend (прежде всего для middleware `getData`).

##### cacheInfo
Middleware отправки данных о дампе другим процессам. Данные отправляются по шине межпроцессного взаимодействия [ipbus](https://doc.yandex-team.ru/si-infra/common_packages/ipbus.html).
Для корректной работы данный мидлвар должен подключаться до мидлваров `cacheReader` и `cacheWriter`.
Также для отображения в интерфейсе [html-reporter-а](https://github.com/gemini-testing/html-reporter) ключа, на основе которого было сгенерировано имя дампа, необходимо, чтобы пользователь в своем мидлваре `cacheFilename` в контекст котика добавил поле `cacheKey`.

Пример реализации мидлвара `cacheFilename`:
```javascript
(req, res, next) => {
    const cacheKey = req.kotik.parsedURL.searchParams.toString();
    req.kotik.ctx.set('cacheKey', cacheKey);
    req.kotik.ctx.set('cacheFilename', `${cacheKey}.json.gz`);
    next();
}
```

Данные о дампе отправляются в следующем формате:
```javascript
{
    testRunId: string; // уникальный id теста
    cacheKey: string; // ключ, на основе которого было сгенерировано имя дампа (обычно ключем является урл)
    cacheFile: string; // путь к дампу на файловой системе
}
```

Чтобы получать данные об используемых дампах, необходимо через `ipbus` подписаться на топик `dumps-cache-info`.

##### cachePath
Middleware определения пути до директории, в которой хранится дамп (поле `cachePath` в контексте).

Поведение по умолчанию зависит от плагина [url-decorator](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/url-decorator):

- Если выставлен флаг `addCacheInfoToTestRunId`, то дамп будет сохранён в директорию, где расположен код теста.
```bash
$ tree features/common/header/
features/common/header/
├── default.hermione.js
├── default.testpalm.yml
├── screens
│   └── 1ef3d56
│       ├── chrome-desktop
│       │   └── header.png
│       ├── chrome-pad
│       │   └── header.png
│       └── chrome-phone
│           └── header.png
└── test-data
    └── 1ef3d56
        ├── chrome-desktop
        │   └── 623637c4bc47d1ecdd7d.json.gz
        ├── chrome-pad
        │   └── 623637c4bc47d1ecdd7d.json.gz
        └── chrome-phone
            └── 623637c4bc47d1ecdd7d.json.gz
```

- В противном случае – в отдельную директорию в корне проекта. По умолчанию - `test-data`, значение можно переопределить опцией.
```bash
$ tree test-data/
test-data/
├── chrome-desktop
│   └── 623637c4bc47d1ecdd7d.json.gz
├── chrome-pad
│   └── 623637c4bc47d1ecdd7d.json.gz
└── chrome-phone
    └── 623637c4bc47d1ecdd7d.json.gz
```

##### cacheReader
##### cacheReaderAppHost
Middleware чтения дампа запроса в AppHost-backend для cacheMode `read` и `create`.

Для чтения используется пакет [file-cacher](https://doc.yandex-team.ru/si-infra/common_packages/file-cacher.html#chtenie-kesha).

Данные ответа будут записаны в контекст котика. [Как работать с данными ответа](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#rabota-s-dannymi-iz-grafa).

##### cacheReaderRegular
Middleware чтения дампа запроса в не-AppHost-backend для cacheMode `read` и `create`.

Для чтения используется пакет [file-cacher](https://doc.yandex-team.ru/si-infra/common_packages/file-cacher.html#chtenie-kesha).

Данные ответа будут записаны в `data` и `meta` поля контекста. [Как работать с контекстом](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#peredacha-dannykh-mezhdu-midlvarami).

##### cacheWriter
##### cacheWriterAppHost
Middleware записи дампа запроса в AppHost-backend для cacheMode `write` и `create`.

Для записи используется пакет [file-cacher](https://doc.yandex-team.ru/si-infra/common_packages/file-cacher.html#zapis-kesha).

[Как работать с данными ответа](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#rabota-s-dannymi-iz-grafa).

##### cacheWriterRegular
Middleware записи дампа запроса в не-AppHost-backend для cacheMode `write` и `create`.

Для записи используется пакет [file-cacher](https://doc.yandex-team.ru/si-infra/common_packages/file-cacher.html#zapis-kesha).

Данные ответа будут записаны из `data` и `meta` полей контекста. [Как работать с контекстом](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html#peredacha-dannykh-mezhdu-midlvarami).

##### compression
Middleware компрессии.

[Подробнее в документации](https://www.npmjs.com/package/compression).

##### connectBusboy
Middleware парсинга multipart/form-data запросов.
Добавляет `req.busboy`. Получение данных происходит в middleware `bodyUnifier`.

[Подробнее в документации](https://www.npmjs.com/package/connect-busboy).

##### cookieParser
Middleware парсинга cookie.
Добавляет `req.cookies` и `req.signedCookies`.

[Подробнее в документации](https://www.npmjs.com/package/cookie-parser).

##### counter
Middleware, проксирующая запросы в clickdaemon для вычисления счетчиков и метрик. В конфигурации `kotik` роутер может выглядеть так:
```javascript
    {
        matcher: req => req.kotik.parsedURL.pathname.startsWith('/clck'),
        handler: [
            { name: 'bodyParserText', fn: middlewares.bodyParser.text() },
            { name: 'counterMiddleware', fn: middlewares.counter() },
        ],
    }
```

##### flushResponse
##### flushResponseAppHost
Middleware, завершающая отдачу ответа на запрос в AppHost-backend: мержит ответы от report-renderer (контент и заголовки).

##### flushResponseRegular
Middleware, завершающая отдачу ответа на запрос в не-AppHost-backend.

##### getData
##### getDataAppHost
Middleware получения данных из AppHost-backend для cacheMode `write`, `create` и без cacheMode.

Данные ответа будут записаны в контекст котика. [Как работать с данными ответа](#rabota-s-dannymi-iz-grafa).

##### getDataRegular
Middleware получения данных из не-AppHost-backend для cacheMode `write`, `create` и без cacheMode.

Данные ответа будут записаны в `data` и `meta` поля контекста. [Как работать с контекстом](#peredacha-dannykh-mezhdu-midlvarami).

##### jsonDump
Middleware просмотра данных, полученных из backend'а/дампа.
Если в url задать параметр `json_dump`, то kotik отдаст json c данным от всех источников (вместо html).

##### render
Middleware рендеринга данных через report-renderer.

Мидлвар обрабатывает поле `clearLoadedTemplates` из контекста котика - флаг очистки списка загруженных шаблонов.
Если он выставлен в `true`, будет выполнена очистка списка загруженных в report-renderer шаблонов. После обработки значение флага будет сброшено в `false`.

##### replaceReqIdAppHost
Middleware подмены reqId для AppHost-backend, необходимая для корректной работы [проверок счетчиков и метрик](https://doc.yandex-team.ru/si-infra/counters-and-metrics/structure.html). Поддерживаемые параметры:

- `getDataReqId(kotikCtx) [function] [optional]` - функция определяет способ получения reqId запроса. Если не указана, используется реализация по умолчанию. На вход получает контекст kotik и выдает reqId.

Мидлвар должен подключаться после получения данных - мидлваров [cacheReaderAppHost](#cachereaderapphost)/[getDataAppHost](#getdataapphost) или аналогичных.

##### replaceReqIdRegular
Middleware подмены reqId для не-AppHost-backend, необходимая для корректной работы [проверок счетчиков и метрик](https://doc.yandex-team.ru/si-infra/counters-and-metrics/structure.html). Поддерживаемые параметры:

- `getDataReqId(kotikCtx) [function] [required]` - функция определяет способ получения reqId запроса. Реализации по умолчанию нет, так как место хранения reqId непредсказуемо. На вход получает контекст kotik и выдает reqId.

Мидлвар должен подключаться после получения данных - мидлваров [cacheReaderRegular](#cachereaderregular)/[getDataRegular](#getdataregular) или аналогичных.

##### serveStatic

Представляет собой обертку над стандартной express-middleware [`serve-static`](https://github.com/expressjs/serve-static). Помимо стандартных для мидлвара опций `root` и `options`, поддерживаются дополнительные необязательные опции:

- `prefixToStrip [string] [optional]` - префикс, который будет оторван от исходного пути запроса (`req.url`) перед передачей в `serve-static` мидлвар в случае совпадения. По умолчанию пустая строка.
- `prefixToAdd [string] [optional]` - префикс, который будет добавлен к пути запроса (`req.url`) в случае, если изначальный запрос совпал по `prefixToStrip`. По умолчанию пустая строка.

Пример:

Для мидлвара с настройками `{prefixToStrip: '/static', prefixToAdd: '/build'}`, запрос к `/static/file.js` будет изменен на `/build/file.js` перед передачей в стандартную express-middleware `serve-static`. Для того же мидлвара запрос к `/users/abc` будет передан в стандартный мидлвар в неизмененном виде.

При передаче следующим мидлварам по цепочке исходный запрос (`req.url`) восстанавливается.

##### templateFlag

Middleware для тестирования вёрстки под флагами. Не может влиять на данные при чтении дампов.

Пререквизиты:

 * Шаблоны должны получать флаги из item с типом `flags` аппхостового контекста.
   Используйте для этого встроенные функции report-renderer для работы с apphost-контекстом - [find*Item](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/renderer/src/lib/ctx/apphost.ts?rev=r8077030#L304-322). Например:
   ```javascript
   apphostCtx.findLastItem('flags')
   ```

Middleware добавляет флаги из параметра котика `templateFlag` (object) в каждый item с типом `flags` для каждого источника.
Проверяет, что в каждом источнике есть необходимый item. Чтобы отключить проверку, нужно передать `false` в параметр котика `checkTemplateFlag` (boolean).

Middleware `templateFlag` нужно использовать после получения данных (middleware `cacheReader` и `getData`) и до начала рендеринга (middleware `render`).

Чтобы url'ы с флагами попали в html отчёт hermionе, используйте плагин [`hermione-exp-flags`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/hermione-exp-flags).

##### templateRewrite

Этот мидлвар — аналог эксп-флага [tmplrwr](https://st.yandex-team.ru/SERP-57904), используется тестирования вебэкспов в hermione. Мидлвар патчит строки в `template_data.name`, что позволяет рендереру загрузить экспериментальный шаблон.

Конфигурация может выглядеть так:

```javascript
    {
        matcher: () => true,
        handler: [
            // ... другие мидлвары ...
            { name: 'getData', fn: middlewares.getData() },
            { name: 'templateRewrite', fn: middlewares.templateRewrite({ from: 'web4', to: 'web_exp3' }) },
            // ... другие мидлвары ...
        ],
    }
```

Тогда, например, при запросе шаблона `web4:desktop` загрузится шаблон `web_exp3:desktop`, потому что `web4` будет заменено на `web_exp3`.

Подробнее про вебэкспы читайте в [документации серпа](https://wiki.yandex-team.ru/serp/release/webexp/).


### Preset

Пресет - это типовой набор мидлваров, который может быть расширен пользовательскими мидлварами или пресетами. Создать свой пресет можно следующим образом:

```javascript
const {Preset} = require('@yandex-int/kotik');

const myPreset = Preset.create('my-preset', [
    {name: 'my-middleware-1', fn: (req, res, next) => {...}},
    {name: 'my-middleware-2', fn: (req, res, next) => {...}}
])
```

Модифицировать пресет можно с помощью методов:

* `addFirst(middlewares)` — добавляет мидлвар/список мидлваров/пресет в начало пресета
* `addLast(middlewares)` — добавляет мидлвар/список мидлваров/пресет в конец пресета
* `addAfter(deps, middlewares)` — добавляет мидлвар/список мидлваров/пресет после последнего мидлвара, указанного в зависимостях (deps)

{% note warning "Внимание!" %}

Не стоит модифицировать пресет, который передаётся в `handler` нескольким роутам. Все роуты получат все изменения пресета.
См. [задачу FEI-14029](https://st.yandex-team.ru/FEI-14029).

{% endnote %}

Пример (используем `myPreset`, объявленный в предыдущем примере):

```javascript
myPreset
    .addFirst({name: 'first', fn: (req, res, next) => {...}})
    .addLast({name: 'last', fn: (req, res, next) => {...}})
    .addAfter('my-middleware-1', {name: 'middle', fn: (req, res, next) => {...}});
```

В итоге мидлвары будут вызваны в следующем порядке: `first`, `my-middleware-1`, `middle`, `my-middleware-2`, `last`.

Чтобы увидеть порядок вызова мидлваров, нужно запустить kotik в режиме `verbose`.

#### Готовые пресеты

* [frontend-static](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/kotik/index.js). Пресет для обработки запросов за статикой.
* [apphost-frontend-dynamic](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/kotik/index.js). Пресет для обработки AppHost-ручек с кешированием.
* [regular-frontend-dynamic](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/kotik/index.js). Пресет для обработки обычных ручек с кешированием.


### Аrchon-компонент kotik

В пакете реализован компонент к [archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html) - `Kot`.
В большинстве случаев вам нужен не сам компонент, а одна из готовых команд:

* [archon-devserver-command](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-devserver-command)
* [archon-renderer-devserver-command](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-renderer-devserver-command)
* [archon-hermione](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-hermione)

Опции компонента:

* `port` - порт http-сервера
* `sslPort` - порт https-сервера
* `cacheMode` - режим работы с дампами:
  * `read` - содержимое контекста читается из дампа, при отсутствии файла возвращается ошибка
  * `write` - содержимое контекста получается из бэкенда и записывается в дамп, существующий дамп перезаписываются
  * `create` - содержимое контекста получается из бэкенда и записывается в дамп, существующий дамп не перезаписывается
* `cacheFile` - путь до дампа, при указании содержимое контекста для всех запросов будет читаться из этого дампа
* `requiredCacheParam` - в режиме cacheMode=read для всех запросов, в которых отсутствует указанный параметр, будет возвращена ошибка
* `verbose` - при указании включает очень подробное логирование
* `workers` - количество процессов, обрабатывающих запросы
* `exitThreshold` - смотри документацию по [luster](https://github.com/nodules/luster#annotated-example-of-configuration)
* `allowedSequentialDeaths` - смотри документацию по [luster](https://github.com/nodules/luster#annotated-example-of-configuration)
* `incognito` - выключает отправку статистики в statface
* `graph` - имя файла с графом (из директории `graphs`), с которым будет выполнен запрос
