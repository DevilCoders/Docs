# Archon

Archon (рус. архон)  - библиотека для построения и исполнения графа процессов. Позволяет автоматизировать выполнение скриптов и бинарей в определенной последовательности. 

Archon разрабатывается для нужд локальной (на ноутбуке) разработки и CI.

Назван в честь юнита из вселенной Starcraft.

```javascript
const http = require("http");

const server = port => ({
    name: "server",
    async init() {
        this.server = http.createServer((req, res) => res.end("OK"));
        return new Promise(resolve => this.server.listen(port, () => resolve({ port })));
    },
    async shutdown() {
        return new Promise(resolve => this.server.close(resolve));
    },
});

const sender = {
    name: "sender",
    async init(results, done) {
        const req = http.request(`http://localhost:${results.get("server").port}`, res => {
            if (res.statusCode === 200) {
                console.log("Response is OK");
                done();
            } else {
                done(new Error(`Bad statusCode ${res.statusCode}`));
            }
        });
        req.on("error", done);
        req.end();
    },
};

module.exports = {
    name: "start-send",
    description: "start server & send request",
    setup(command) {
        command.options({
            // see yargs package
            port: {
                type: "number",
                required: true,
            },
        });
    },
    graph(options) {
        return [server(options.port), { ...sender, deps: ["server"] }];
    },
};
```

Структура конфигов – в [примере](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/archon/src/__fixtures__/project-readme).

## Мотивация

При разработке зачастую нужно поднять более одного процесса. Например, для запуска тестов в web4 (шаблоны поиска по вебу) нужно:
* запустить hermione с тестами, она требует:
  * dev-сервер
    * renderer с кодом шаблонов из папки разработчика 
    * [tunneler](https://doc.yandex-team.ru/si-infra/tunneler/tunneler.html) (процесс, предоставляющий публично доступные адреса; аналог ngrok)
  * [clickdaemon](https://wiki.yandex-team.ru/logs/clickdaemon/) (процесс, обрабатывающий клики по результатам выдачи)
  * [metricsdaemon](https://wiki.yandex-team.ru/logs/calcmetricsdaemon/) (процесс, считающий метрики по логам "как в проде")
  * процесс для очистки логов

Запущенные процессы нужно правильно связать между собой. Например, dev-серверу нужно передать порт, на котором запущен renderer. Всем процессам нужно передать один и тот же путь до папки с логами. Hermione должна использовать путь до файла с логами clickdaemon, а dev-сервер должен подставлять в отдаваемые страницы правильный адрес, по которому доступен clickdaemon.

Для решения этих задач и создан Archon.
* процесс описывается Archon-компонентом
* Archon позволяет нужным образом скомпоновать команды из компонентов
* Archon становится единой точкой входа для инструментов разработки и тестирования на проекте: оказавшись на проекте,
где есть Archon, можно сразу посмотреть все имеющиеся команды, а не искать по конфигурациям и документациям в различных папках проекта
* компоненты и команды могут переиспользоваться и распространяться как в виде отдельных модулей, так и в составе проекта.

Archon избавляет команду от описывания логики в bash скриптах или сложных npm-командах, дает единое удобное api для автоматизации процессов разработки.

{% cut "Неинтересная историческая часть" %}

[Темплар](https://doc.yandex-team.ru/si-infra/local_devserver/templar.html) создавался, как сервер
для локальной разработки для SERP. С тех пор появились новые проекты и, как результат, новые хотелки, которые сложно
(если вообще возможно) реализовать в архитектуре, рассчитанной только на СЕРП. Это привело к появлению множества
костылей на стороне или проектов или темплара.

Накопилось достаточно задач, которые сложно решать в темпларе:

* запуск произвольных сервисов, уникальных для проекта (всевозможные fs-watcher-ы, кликдемон, прокси, websocket-сервисы и т.п.)
* скачивание ресурсов, уникальных для проекта
* кастомизация сервера локальной разработки для сервисов, отличных от SERP по своему устройству (например, чаты)
* переиспользование полезных частей темплара, если в остальном сервер разработки не нужен (скачивание ресурсов, туннелер для раздачи статики в лего)

Для решения обозначенных задач и был создан Archon.

{% endcut %}

### Почему не ...?

* ... task runner?
  Посмотрим на разницу на примере поднятия бэка, фронта и запуска тестов на фронт.
  Task runner позволит поднять бэк и фронт, затем запустить тесты, но если что-то пойдёт не так, нужно будет как-то отдельно зачищать недоподнятые окружения.
  При этом Archon позволяет ясно описать и старт компонента, и штатное/аварийное завершение компонента, а вызовутся эти методы автоматически.

* ... docker compose?
  Опять же, посмотрим на разницу на примере поднятия бэка, фронта и запуска тестов.
  Docker Compose позволяет поднять окружение (бэк + фронт) одной командой, запустить тесты и погасить также одной командой; итого 3 команды.
  Archon позволяет всё это сделать одной командой, даже, например, поверх Docker Compose: один компонент для окружения с вызовами старта/шатдауна и второй для запуска тестов.
  
  К тому же, в случае, если поднятие Docker-контейнера не означает готовность сервиса к работе, приходится создавать
  дополнительные команды, которые после старта контейнера ожидают выполнения некоторых условий, например, [wait-for](https://github.com/eficode/wait-for).
  В случае с Archon подобное ожидание выполняется в методе init.

* ... makefile?
  Нет явной передачи данных от одних компонентов другим, это инструмент из мира backend-разработки (среднестатистический frontend-разработчик не умеет читать и писать makefiles), нет завершения работы процессов в порядке, обратном активации.

* ... bash?
  Зачем писать код на bash, когда можно писать его на js?

## Основные понятия

**Компонент** отвечает за выполнение атомарного полезного действия. Например, выполнение небольшого скрипта, старт сервиса (скачивание ресурса Sandbox, запуск DNS-сервера, ...).

Жизненный цикл компонента:
```
(все зависимости запущены) -> init -> (resolve) -> продолжаем выполнение графа
                                \_______ (reject)
                                        ]----------------->terminate
                                       / (reject)
(все зависящие завершили работу) -> shutdown -> (resolve) -> продолжаем завершение графа
(вызов done) -> граф завершает работу
```

При init компоненты получают на вход данные компонентов, указанных у них в зависимостях. Например, сервер при старте получает путь до запускаемого файла от компонента, который запускает сборку. Путь до логов пользователь указывает в аргументах командной строки, его должна передать команда при создании компонента.
Init компоненты возвращает промис с данными, которые могут быть использованы зависящими от них компонентами.

Компонент может выполнить разовое действие (скачать файл), а может активно работать (запустить процесс и взаимодействовать с ним). В таком случае помимо окончания инициализации ему нужен способ сообщить, что его работа завершена. Для этого в init передаётся функция done.

Например, для старта report-renderer должен знать порт, на котором запущен clickdaemon. Поэтому компонент,
отвечающий за процесс clickdaemon, должен в выходные данные init включить номер порта, на котором clickdaemon стартовал,
а компонент, отвечающий за report-renderer, должен использовать эти данные для поднятия report-renderer.

При shutdown компонент очищает за собой оставленные в ОС артефакты. Если компонент не снимет все обработчики внешних событий, то процесс не выйдет. Archon не предпринимает каких-то попыток почистить всё вместо компонента.

Если на этапе activate или shutdown случается ошибка, вызывается terminate. Как правило, на этом этапе делается то же самое, что и в shutdown, но сильнее. Например, запущенный процесс можно завершить при помощи SIGKILL, а не SIGTERM.

Взаимодействие компонентов происходит только двумя способами: через данные для init или через [шину сообщений ipbus](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/ipbus).

**Команда** объединяет компоненты в дерево зависимостей одних компонентов от других и предоставляет cli для удобного запуска. Вызов init компонентов производится начиная с компонентов без зависимостей.

Такая организация позволяет для каждого проекта собрать свои команды со своим набором компонентов.

Например, в одной команде можно выразить поднятие dev-сервера: скачивание необходимых ресурсов, запуск процессов
clickdaemon, report-renderer и kotik в правильной последовательности.

В другой команде может быть запуск тестов: поднятие dev-сервера, запуск hermione, скачивание необходимых тестовых данных.

Все команды добавляются в конфиг архона и доступны из cli: `npx archon --help`.

Команды [можно переиспользовать](#kak-pereispolzovat-komandu).

## Tutorial

Пример можно найти в [документации](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_tutorial.html).

## Известные команды и компоненты

Собраны [в доке](https://doc.yandex-team.ru/si-infra/local_devserver/archon/).

## Как это все работает

Рассмотрим на примере такого графа компонентов:

```js
[
    {name: 'A', deps: ['B', 'C']},
    {name: 'B', deps: ['D']},
    {name: 'C', deps: ['D', 'E']},
    {name: 'D'},
    {name: 'E'}
]
```

![Graph](https://a.yandex-team.ru/api/v1/repos/arc_vcs/tree/blob/frontend/projects/infratest/packages/archon/images/graph.png?commit_id=r8895460)

При запуске команды вызывается init компонентов - этот этап называется активацией. При ошибке во время активации или работы или при останове происходит деактивация.

### Активация

Вызов init компонентов происходит в порядке от листьев к корням леса, причем init компонента стартует в тот момент,
когда init всех его зависимостей завершился.
В данном случае первой стартует инициализация компонентов D и E. Как только завершится активация компонента D, начнётся
активация компонента B. И так далее.

Активация выполняется вызовом метода `init` компонента, в который передаются результаты выполнения `init` его зависимостей.
Таким образом можно передавать информацию от компонента к компоненту при старте.

### Деактивация

Деактивация происходит в порядке от корней к листьям леса.

В данном случае первой начнётся деактивация компонента A. После его деактивации начнётся деактивация компонентов B и C. И так далее.

Деактивация выполняется при помощи вызовов `shutdown` и `terminate` компонентов: сначала вызывается `shutdown`,
и затем в случае неуспешного `shutdown` вызывается `terminate`.


## Настройка Archon

Для настройки Archon на проекте необходимо выполнить следующие шаги:

1. добавить `@yandex-int/archon` в зависимости проекта,
1. настроить директорию с конфигурацией Archon в `.yproject`,
1. создать проектный конфигурационный файл.

Также Archon подгружает данные из пользовательского конфигурационного файла, расположенного по пути
`~/.config/archon/config.json`. При помощи него можно задавать пользовательские команды.

### .yproject в корне проекта

В корневой директории проекта должен быть файл `.yproject`, содержимое которого представляет собой валидный JSON.

В файле должен быть указан путь к папкам с настройками Archon, в корне которого лежит конфигурационный файл Archon.

```json
{
    "paths": {
      "archon": "./.config/archon"
    }
}
```

### Конфигурационный файл Archon

Конфигурационный файл `config.json` должен находиться в корне папки с настройками Archon, содержимое которого представляет собой валидный JSON.

#### commands

В данном поле указывается список команд проекта в виде массива путей для require. Это может быть файл модуля
или путь на FS, абсолютный или относительный (`.` - папка с `config.json`).

```json
{
    "commands": [
        "@yandex-int/internal-cert/commands/cert",
        "@yandex-int/local-dns/commands/start",
        "@yandex-int/local-dns/commands/settings"
    ]
}
```

Каждая добавленная в конфигурационном файле команда добавляется в список команд Archon и становится доступна в Archon CLI.
Название команды берется из её описания. Например, так выглядит `help` для приведенной выше настройки проектных команд:

```
  $ npx archon --help
  Usage: archon [command] [options]

  Utility for components composition

  Options:

    -V, --version               output the version number
    -h, --help                  output usage information

  Commands:

    cert [options]              Генерация сертификатов
    dns-server-start [options]  Запуск локального DNS-сервера
    local-dns-setup [options]   Настройка локального DNS для OSX и Ubuntu

  Чтобы получить более подробную справку по каждой из команд, наберите archon [command] --help
    например: archon start --help
```

## Создание команд и компонентов

В данном разделе содержится справочная информация о том, какие есть возможности при реализации команд и компонентов.

Также есть отдельный [Tutorial](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_tutorial.html), где показано, как собрать первые несложные команды.

Предполагается, что компоненты и команды для Archon будут поставляться в виде отдельных пакетов. В каждом таком пакете
будут находиться компоненты, предназначенные для решения одной задачи или группы сильно связанных между собой задач,
а также в нем будут находиться команды, запускающие выполнение этих компонентов, если такая необходимость есть.

Примером могут послужить пакеты [internal-cert](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/internal-cert.html) (работа с внутренними сертификатами) и
[local-dns](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/local-dns.html) (работа с настройками локального DNS и компонент, отвечающий за процесс локального DNS-сервера).

Эталонная архитектура пакета с компонентами и командами предполагает, что файлы с компонентами будут находиться в папке
`components`, а файлы с командами - в папке `commands`. При этом модуль, являющийся точкой входа в пакет, экспортирует
объект с полем `components` (хеш с компонентами) для удобства использования их в командах проекта или другого модуля.
О формате описания компонента можно прочитать [здесь](#kak-opisat-komponent).
Команды не экспортируются, так как в конфигурацию Archon они включаются по прямому пути до файла с командой.
О том, как описать команду, можно прочитать [здесь](#kak-opisat-komandu).

Для создания одной команды могут использоваться другие команды. Как описать команду с использованием других команд и как
описывать переиспользуемые команды можно подробнее прочитать в [здесь](#kak-pereispolzovat-komandu).

### Как описать компонент

Компонент – объект, удовлетворяющий [интерфейсу Component](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/archon/src/component.ts), описывается при помощи следующих полей:

* [name](#componentname)
* [deps](#componentdeps)
* [transformInput](#componenttransforminput)
* [init](#componentinit)
* [initTimeout](#componentinittimeout)
* [shutdown](#componentshutdown)
* [shutdownTimeout](#componentshutdowntimeout)
* [terminate](#componentterminate)
* [terminateTimeout](#componentterminatetimeout)

Примеры (описания компонентов есть в README соответствующих модулей):

* [dns-settings-create](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/local-dns/src/commands/settings.ts)
* [dns-settings-cleanup](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/local-dns/src/components/cleanup.ts)
* [dns-server](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/local-dns/src/components/server.ts)
* [kotik](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/kotik/components/kot.js)

#### component.name

*Required*. Имя компонента.

#### component.deps

*Optional*. Список имён компонентов, от которых зависит данный компонент.

*По умолчанию*: пустой список.

#### component.transformInput

*Optional*.
Функция для преобразования выходных данных [компонентов-зависимостей](#componentdeps)), в подходящий для данного компонента формат. 
На вход функция получает один аргумент - `Map` с именами инициализировавшихся компонентов в качестве ключей
и выходными данными метода [component.init](#componentinit) этих компонентов в качестве значений.
Результат выполнения `transformInput` подаётся на вход метода [component.init](#componentinit) текущего компонента в параметр `results`.

*По умолчанию*: никаких преобразований не применяется.

#### component.init

*Optional*. Функция, описывающая инициализацию компонента, которая должна возвращать `Promise`.
На вход функция получает два аргумента:
* первый - `results` – объект, подготовленный методом [component.transformInput](#componenttransforminput), или 
оригинальный `Map` с именами инициализировавшихся [компонентов-зависимостей](#componentdeps) в качестве ключей 
и выходными данными метода `component.init` этих компонентов в качестве значений.
* второй - `done` – функция, которая должна быть вызвана для завершения команды; для штатного - без аргументов,
при ошибке – с ошибкой в качестве аргумента.

При резолве Promise должен вернуть данные, необходимые для инициализации зависящих от данного компонентов.

*По умолчанию*: no-op.

#### component.initTimeout

*Optional*. Таймаут выполнения `init`. Если таймаут равен 0, то операция не лимитируется по времени.
 
*По умолчанию*: 30с.

#### component.shutdown

*Optional*. Функция, описывающая штатное завершение работы компонента, которая должна возвращать `Promise`.

*По умолчанию:* no-op.

#### component.shutdownTimeout

*Optional*. Таймаут выполнения `shutdown`. Если таймаут равен 0, то операция не лимитируется по времени.

*По умолчанию:* 5с.

#### component.terminate

*Optional*. Функция, описывающая аварийное завершение работы компонента, которая должна возвращать `Promise`.

*По умолчанию:* no-op.

#### component.terminateTimeout

*Optional*. Таймаут выполнения `terminate`. Если таймаут равен 0, то операция не лимитируется по времени.

*По умолчанию:* 1с.

### Как описать команду

Команда - объект, удовлетворяющий [интерфейсу Command](https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/archon/src/command.ts), имеет следующие свойства:

* [name](#commandname)
* [description](#commanddescription)
* [usage](#commandusage)
* [setup](#commandsetup)
* [options](#commandoptions)
* [graph](#commandgraph)

Примеры (описания команд есть в README соответствующих модулей):

* [cert](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/internal-cert/commands/cert.js)
* [local-dns-setup](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/local-dns/src/commands/settings.ts)
* [dns-server-start](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/local-dns/src/commands/start.ts)
* [kotik](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-renderer-devserver-command/commands/kotik.js)

#### command.name

*Required*. Строка с именем команды.

Важно понимать, что имя должно быть уникальным среди всех команд проекта и пользовательских.

#### command.description

*Optional*. Строка с описанием команды, которая будет использована при выводе help'а.

#### command.usage

*Optional*. Строка с описанием использования команды и прочая информация, которая будет показана при выводе помощи.

#### command.setup

*Optional*. Метод, который на вход получает инстанс [yargs](https://www.npmjs.com/package/yargs) или объект с конфигом опций команды.
Можно не указывать, тогда у команды не будет своих опций.

#### command.options

*Optional*. Объект с описанием опций в формате описания опций [yargs](https://www.npmjs.com/package/yargs).

#### command.graph

*Required*. Метод, который на вход получает объект с опциями и возвращает массив с описанием графа зависимостей компонентов.

Опции вычитываются из различных источников, и эти источники по приоритетам распределены следующим образом:

1. Переменные среды окружения. В опции попадают только переменные среды окружения, имя которых начинается с `ARCHON_`,
при этом их имена преобразуются в camelCase: `ARCHON_LONG_NAME -> longName`.
1. Опции командной строки.
1. Опции из проектного конфига.
1. Опции из пользовательского конфига.

Граф должен описывать все используемые компоненты и быть деревом (или лесом). Каждый элемент массива – это описание
компонента.

### Как переиспользовать команду

Переиспользование команды предполагает включение опций и графа компонентов этой команды в список опций и граф
компонентов использующей её команды.

Если команду предполагается переиспользовать, то все опции, которые должны будут оказаться в переиспользующей команде,
должны быть перечислены в свойстве `options`.
Эти опции должны иметь уникальные имена, которые позволят избежать конфликта опций при встраивании в другую команду
(но могут иметь более короткие алиасы, которые будут использованы при обычном запуске команды).

В функции построения графа эти опции должны использоваться по их полным именам, так как при встраивании алиасы будут
устранены. Например, опция `workers` в команде запуска renderer может называться `rendererWorkers`, и она должна
использоваться по этому имени вне зависимости от того, какие у нее есть алиасы.

[Пример команды, подготовленной для переиспользования](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/commands/reusable-command.js)

Для того, чтобы включить одну команду в другую, нужно:
* добавить в список опций текущей команды опции переиспользуемой команды при помощи функции `inheritOptions`,
* добавить в граф текущей команды граф переиспользуемой команды и указать необходимые зависимости при помощи функции `addEdges`.

[Пример команды, переиспользующей команду из примера выше](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/commands/reusing-command.js)

Пример реального использования можно посмотреть в команде [kotik](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-renderer-devserver-command/commands/kotik.js),
которая переиспользует команду [renderer](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-renderer/commands/renderer.js).

Доступные из коробки утилитные функции экспортируются из [файла](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon/src/utils.ts) и могут использованы, как показано в примерах выше.

## Дебаг

Дебажные логи пишутся при включении переменной окружения `DEBUG='si:archon:*'`. Как правило, переменная окружения `DEBUG` поддержана во всех компонентах и при включении `DEBUG=*` можно увидеть огромную гору дебажных логов.

### Почему процесс Archon не завершается?

`DEBUG='si:why-is-archon-running'` включет вывод [wtfnode](https://www.npmjs.com/package/wtfnode). Пример вывода:
```
[WTF Node?] open handles:
- File descriptors: (note: stdio always exists)
  - fd 1 (tty) (stdio)
  - fd 2 (tty) (stdio)
- Child processes
  - PID 4392
    - Entry point: /Users/catwithapple/Projects/Yandex/infratest/node_modules/ssh-tun/index.js:68
    - STDIO file descriptors: 13, 25
```

`DEBUG='si:si:why-is-archon-running:verbose'` включает вывод [why-is-node-running](https://www.npmjs.com/package/why-is-node-running).  Пример вывода:
```
There are 33 handle(s) keeping the process running

# SIGNALWRAP
/Users/catwithapple/Projects/Yandex/infratest/packages/archon/lib/cli.js:115 - process.on(signal, async () => {
/Users/catwithapple/Projects/Yandex/infratest/packages/archon/lib/cli.js:114 - ['SIGHUP', 'SIGINT', 'SIGTERM'].forEach((signal) => {

# TLSWRAP
/Users/catwithapple/Projects/Yandex/infratest/node_modules/got/source/request-as-event-emitter.js:234 - handleRequest(fn.request(options, handleResponse));
/Users/catwithapple/Projects/Yandex/infratest/node_modules/got/source/request-as-event-emitter.js:305 - await get(options);

...
```
