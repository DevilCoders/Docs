# sandbox-resource-helpers

Пакет для скачивания sandbox-ресурсов.
Может скачивать ресурсы по http или для sandbox задач - через [synchrophazotron](https://wiki.yandex-team.ru/sandbox/cookbook/#kakpoluchitdannyesinxronizirovatresursizpodprocessazadachi).
Поддержано фоновое скачивание файлов для обновления ресурсов.
Скачанные файлы из sandbox по http проверяются по md5 хешу (не всегда он есть).
Если запрос в sandbox за метаданными о ресурсе или установка ресурса завершилась с ошибкой, то будет взят последний ресурс их кеша, подходящий под фильтры.

Директория с логами по умолчанию: `~/.yandex-int/logs`.

## Пререквизиты

```javascript
npm i --save @yandex-int/sandbox-resource-helpers --registry https://npm.yandex-team.ru
```

**Важно:** для использования из Trendbox/Qloud/etc. необходимо получить токен Sandbox и установить его в переменную `SANDBOX_AUTH_TOKEN`.

## Пример использования

Допустим, нам надо скачать последнюю релиз-версию report-renderer+ynode: ресурс с типом `REPORT_RENDERER_BUNDLE`.

```javascript
const { SandboxResource } = require('@yandex-int/sandbox-resource-helpers');

const res = new SandboxResource({
    // имя ресурса в терминах Sandbox
    name: 'REPORT_RENDERER_BUNDLE',

    // префикс для переменных окружения
    // по умолчанию равно полю "name"
    // envVarsPrefix: 'MY_SHORT_PREFIX',

    // в мс, по умолчанию не ограничен
    timeout: 30000,

    // стратегия обработки ресурса (file, executable, tar или directory)
    // стратегию нужно определить самостоятельно, изучив целевой ресурс
    // по умолчанию tar
    strategy: 'tar',

    // фильтрация по атрибутам
    filter: {
        attrs: {
            released: 'stable',
        },
    },

    // укажите backgroundDownload === true, если нужна возможность фоновой загрузки ресурса.
    backgroundDownload: false,
});

(async function() {
    // укажите reuse === true, если нужно отключить обновление ресурса
    await res.install({ reuse: false });

    // путь для директории, куда распаковался архив с ресурсом
    // здесь сейчас есть баг: последнюю поддиректорию в пути надо отрезать :(
    // фикс будет в https://st.yandex-team.ru/FEI-12242
    console.log(res.path);
})();
```

**NB:** Подробнее про фильтрацию смотрите [в swagger-документации Sandbox](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/resource).

## Фоновая загрузка ресурсов

По умолчанию возможность фоновой загрузки отключена. Чтобы включить, укажите параметр `backgroundDownload: true` в конструкторе.
Работает следующим образом:

-   если в кеше есть старый ресурс, подходящий под фильтры, то возвращается путь до него и запускается скачивание файла для обновления в [detached](https://nodejs.org/api/child_process.html#child_process_options_detached) процессе.
-   если есть скачанный в фоне файл для обновления ресурса, то ресурс устанавливается.
-   если есть скачанные в фоне файлы для обновления нескольких ресурсов, то установится самый свежий из ресурсов.
-   если при скачивании файла в фоне произошла ошибка, то текст ошибки будет выведен в console основного процесса. На работоспособность или скорость работы ошибка скачивания не влияет.

Подробные логи фоновой загрузки в `~/.yandex-int/logs/sandbox-resource-helpers`.

Поддержано фоновое обновление связанных между собой ресурсов (например, ynode и report-renderer). Загруженный в фоне ресурс не будет устанавливаться до тех пор, пока не установлены все dependencies ресурсы.
Dependencies ресурсы задаются в конструкторе SandboxResource.

## Переменные окружения

-   `YANDEX_INT_RESOURCES_PATH` - путь до корневой директории, в которой будут размещены кеш ресурсов sandbox и логи утилит. По умолчанию `~/.yandex-int/`.
-   `SBH_SKIP_UPDATE` - если переменная задана, то по возможности используются ресурсы из локального кеша.
-   `SBH_DISABLE_BACKGROUND_DOWNLOAD` - если переменная задана, то отключается возможность фоновой загрузки для всех ресурсов.
-   `SYNCHROPHAZOTRON_PATH` (`SANDBOX_SYNCHROPHAZOTRON_PATH`) - путь до синхрофазатрона. Если не задан, то скачивание будет по http.
-   `SBH_API_RETRIES` - количество попыток для запросов получения метаданных ресурса и скачивания ресурса, по умолчанию 15.
-   `SBH_API_TIMEOUT` – timeout для запроса получения метаданных ресурса от sandbox, в мс, по умолчанию 60000.
-   `SBH_API_MIN_RETRIES_TIMEOUT` - время до старта первого ратрая для запроса получения метаданных ресурса от sandbox, в мс, по умолчанию 500.
-   `SBH_API_MAX_RETRIES_TIMEOUT` - максимальное время между двумя ретраями для запроса получения метаданных ресурса от sandbox, в мс, по умолчанию 2000.

### Переменные окружения для конкретного ресурса

Для каждого ресурса есть несколько переменных окружения. Префикс для них задается в конструкторе параметром `envVarsPrefix`.

-   `<envVarsPrefix>_RESOURCE_ID` – игнорировать фильтры и скачивать ресурс с указанным ID.
-   `<envVarsPrefix>_DOWNLOAD_TIMEOUT` – timeout на скачивание ресурса, по умолчанию timeout не задан.
-   `<envVarsPrefix>_RESOURCE_PREPARED` - путь до подготовленного ресурса. Возлагаем на клиента всю ответственность за корректность и актуальность ресурса, не проверяем ничего, даже факт установки ресурса.

Пример 1. Нужно использовать переменную окружения MY_SHORT_PREFIX_RESOURCE_ID для того, чтобы задать для загрузки конкретный ID ресурса, объявленного следующим образом:

```
const res = new SandboxResource({
    name: 'REPORT_RENDERER_BUNDLE',
    envVarsPrefix: 'MY_SHORT_PREFIX',
    ...
});
```

Пример 2. Нужно использовать переменную окружения REPORT_RENDERER_BUNDLE_DOWNLOAD_TIMEOUT для того, чтобы задать timeout загрузки файла ресурса, объявленного следующим образом:

```
const res = new SandboxResource({
    name: 'REPORT_RENDERER_BUNDLE',
    ...
});
```
