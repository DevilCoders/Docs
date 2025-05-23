# Renderer courier

Утилита для обновления шаблонов (и произвольных файлов для их работы) в сервисах под управлением renderer.

Позволяет обновлять данные без выключения всего инстанса. Это возможно благодаря [динамическим ресурсам](https://wiki.yandex-team.ru/runtime-cloud/nanny/howtos/structured-instancectl-config-how-to/#notify-action). Если разметить шаблоны и данные флагом `is_dynamic`, то при обновлении только динамических ресурсов будет сделан http-запрос на http-сервер, запущенный курьером, вместо остановки контейнера и подготовки нового. Эта утилита при получении запроса выполняет необходимые для обновления ресурсов действия: подготавливает папку с новыми ресурсами и вызывает `soft-restart` у renderer.

Посмотреть преимущества курьера можно [на примере квадратов](./docs/demo.md).

## Использование

### CLI

* `courier -c <config file> prepare` – подготовит все необходимые для работы данные и соберет рабочую папку
* `courier -c <config file> watch` – запустит сервер, который при каждом вызове /update будет пересобирать рабочую папку и перезапускать renderer

Сервер предполагает, что перед его запуском был вызван `prepare`. Если вызвать `watch` без `prepare`, что-нибудь сломается.

### Интеграция в nanny

Описана в [docs/nanny.md](./docs/nanny.md).

## Пример работы

Пример конфигурации приведен в файле config.example.json в корне репозитория.

Далее этот файл будет называться config.json:
```js
{
    // Адрес, на котором будет запущен http-сервер
    "host": "::",
    // Порт, на котором будет запущен http-сервер
    "port": 90,
    // Папка, внутри которой courier будет хранить все свои данные
    "workingDir": "courier-data",
    // Максимальное значение случайной задержки перед вызовом soft-restart, мс
    "restartDelayUpperBound": 60000,
    // Наборы ресурсов
    "workplaces": [
        {
            // Папка, в которую будет собрана текущая версия всех сконфигурированных в наборе ресурсов
            "path": "resources-prepared",
            // Команда, которая будет выполняться для проверки новой версии ресурсов
            "testCommand": "./ynode/bin/ynode --min_semi_space_size=64 --max_semi_space_size=64 --max_old_space_size=1024 ./report-renderer/node_modules/luster/bin/luster.js ./report-renderer/config.js --logs /logs --logs-suffix selftest --workers 1 --templates-package \"${RESOURCE_DIR}/*/routes.js*\" --self-test",
            // Сконфигурированные ресурсы
            "resources": [
                {
                    // Путь на файловой системе
                    "path": "web4.tar.gz",
                    // Путь внутри рабочей папки, куда будет помещен подготовленный ресурс. Для архивов можно указывать путь только из одного сегмента.
                    "target": "web4",
                    // Этот ресурс нужно распаковать
                    "preparation": {
                        // Возможные значения: "unpack", "symlink"
                        "type": "unpack",
                        // Отрезать первый компонент из пути файлов в архиве. Опция не обязательная, по умолчанию пути не модифицируются.
                        "strip": 1
                    }
                },
                {
                    // Путь на файловой системе
                    "path": "geodata",
                    // Путь внутри рабочей папки, куда будет помещен подготовленный ресурс. Для ссылок можно указывать произвольный путь.
                    "target": "geodata",
                    // На этот ресурс будет установлен symlink
                    "preparation": {
                        "type": "symlink"
                    },
                    // Этот ресурс может отсутствовать. Если такое произойдёт, то весь workplace будет удалён, сборка других workplaces продолжится.
                    "required": false,
                }
            ],
            // Настройки админских ручек report-renderer, которые нужно перезапустить при обновлении ресурсов. 
            "renderers": [
                {
                    // Адрес ручки в формате host:port
                    "endpoint": "[::1]:80",
                    // Максимальное время, которое отводится на soft-restart. Если превышено, ресурсы будут откачены и вызван новый soft-restart, мс
                    "restartTimeout": 600000
                },
                {
                    // Адрес ручки в формате host:port
                    "endpoint": "[::1]:85",
                    // Максимальное время, которое отводится на soft-restart. Если превышено, ресурсы будут откачены и вызван новый soft-restart, мс
                    "restartTimeout": 600000
                }
            ]
        }
    ]
}
```

Один и тот же ресурс допускается использовать в разных `workplaces`, однако все настройки `preparation` для них должны совпадать - в противном случае курьер упадёт с ошибкой на этапе чтения конфига.

### prepare

Команда `courier -c config.json prepare` выполнит следующее:
* очистит служебные папки и файлы внутри `courier-data` (поле `workingDir` конфига), в том числе удалит папку с распакованными ресурсами
* очистит папку `resources-prepared` (поля `workplaces.path` конфига для каждого из `workplaces`)
* файл по пути `web4.tar.gz` от `cwd` распакует в служебную папку внутри `courier-data`, отрезав из путей, указанных в архиве, по одному компоненту (параметр `"strip": "1"`)
* внутри папки `resources-prepared` создаст симлинки:
  `web4` -> папка с распакованным содержимым `web4.tar.gz`, например ` /путь_до_сервиса_в_nanny/courier-data/unpacked-resources/web4.tar.gz_018abc808ab80/42efcbf257e860e9500516229730d00f/`
  `geodata` -> `realpath` до `geodata`, например `/путь_до_скачанных_ресурсов_в_nanny/dynamic/bbdd49a06f081187f101dd3fb4cc94b7bf6c7312_r5P61h3shMG/geodata`
* в служебный файл внутри папки `courier-data` запишет контрольные суммы файлов `web4.tar.gz` и `geodata`

### watch

Команда `courier -c config.json watch` выполнит следующее:
* прочитает контрольные суммы файлов `web4.tar.gz` и `geodata` из служебного файла внутри папки `courier-data`
* выполнит обновление ресурсов. Это нужно, чтобы корректно запускаться в случаях, когда обновление ресурсов было сделано через остановку секций. Подробнее в https://st.yandex-team.ru/FEI-16379.
* запустит http-сервер на хосте `::` (поле `host`) и порту `90`

Сервер:
* при запросе на `/update` сверит контрольные суммы файлов `web4.tar.gz` и `geodata` с запомненными ранее
* если контрольные суммы совпадают, ответит кодом 200
* если контрольные суммы не совпадают, начнет обновление ресурсов

Обновление ресурсов:
* если файл `web4.tar.gz` изменился, то он будет распакован в новую папку внутри `courier-data`
* в служебной папке `courier-data/temp/some-unique-folder-name` будут созданы симлинки, как это делается для папки `resources-prepared`
* будет запущена команда `RESOURCE_DIR="courier-data/testDir" ./ynode/bin/ynode ....` (поле `testCommand` конфига `workplace`)
* симлинки и проверка выполняются последовательно для каждого из `workplaces` в конфиге
* если хотя бы одна из команд проверки завершится с ненулевым кодом, обновление ресурсов прекратится:
  * все созданные в процессе обновления файлы будут удалены
  * на http-запрос будет ответ с кодом 500
  * TODO https://st.yandex-team.ru/FEI-15666: добавить таймаут на выполнение команды
* ожидание случайной задержки от 0 до 60000мс (поле `restartDelayUpperBound`),
* папка `resources-prepared` будет заменена на `courier-data/temp/some-unique-folder-name`
* будет вызван `soft-restart` для renderer, запущенного на `[::1]:80` (поле `endpoints` конфига)
* после завершения будет вызван `soft-restart` для renderer, запущенного на `[::1]:85`
* замена папки и вызов `soft-restart` будет повторён для каждого из настроенных `workplaces`
* если любой из вызовов `soft-restart` завершится с ошибкой или превысит 600000мс (поле `restartTimeout`), будет откат всех ресурсов к предыдущей версии:
  * возвращено прошлое состояние папки `resources-prepared` и 
  * вызван `soft-restart` для всех `renderer` у тех `workplaces`, для которых уже было сделано обовление
  * на http-запрос будет ответ с кодом 500
* на http-запрос будет ответ с кодом 200

Все `workplaces` находятся либо в состоянии, которое было до вызова `/update`, либо в новом состоянии. Промежуточное допускается только во время обработки `/update`.

После окончания обновления (успешного или неуспешного), удаляются все **подготовленные (распакованные)** ресурсы, которые не используются в текущем состоянии.

Случайная задержка перед вызовом `soft-restart` позволяет избежать пиковых нагрузок при одновременном перезапуске renderer во всем кластере. Есть смысл использовать её при невозможности настроить `operation_degrade_level` в Nanny. 

### waitingforsquashfs
Команда `courier -c config.json waitingforsquashfs` выполнит следующее:
* прочитает информацию о примонтированных дирректориях из `courier-data`
* дождётся пока они станут примонтироваными


## Подготовка ресурсов

### unpack

`unpack` всегда распаковывает в папку `target`. Нет способа распаковать данные непосредственно в `workingDir`.

В поле `target` можно указать путь только из одного сегмента. Если будет указано более одного сегмента – чтение конфига упадет с ошибкой. Это ограничение существует только из-за того, что на этот путь завязана структура папок в `unpacked-resources` и очистка неиспользуемых версий ресурсов. 

Все абсолютные пути в архиве будут превращены в относительные (отрезается начальный `/`).

Пути, ведущие наверх (`..`), не распаковываются.

Распаковка делается пакетом [tar](https://www.npmjs.com/package/tar#tarxoptions-filelist-callback-alias-tarextract)

Ресурс распаковывается во временную папку, если эта операция завершилась успешно – папка с распакованными файлами перемещается в `unpacked-resources`. Это гарантирует, что в `unpacked-resources` не будет частично распакованных ресурсов и их можно безопасно переиспользовать.

При обновлении в первую очередь проверяется, есть ли уже распакованная версия ресурса с той же контрольной суммой в папке `unpacked-resources`. Если есть, то повторно ресурс не распаковывается.

После каждого обновления все неиспользованные распакованные ресурсы удаляются.

### symlink

По пути `resources-prepared/target` размещает symlink на `realpath(path)`.

В поле `target` можно указать путь только из нескольких сегментов. Пример:
```json
{
    "path": "news_report_data_current/news_report_data_PROD",
    "target": "news_report_data/current",
    "preparation": {
        "type": "symlink"
    }
}
```
При такой конфигурации в рабочей папке будет создан файл `news_report_data/current`, указывающий на `realpath(news_report_data_current/news_report_data_PROD)`.

### mount

На данный момент доступно монтирование только squashfs-образов,

`mount` выполняет монтирование в директорию `/squash_fs/...` 

Монтирование выполняется при помощи утилиты [portoctl](https://github.com/yandex/porto/blob/master/porto.md)

Ресурс монтируется в директорию для образов, после чего в `resources-prepared` создаётся символьная ссылка на примонтированный образ с ресурсом ресурс.

При обновлении в первую очередь проверяется, есть ли уже примонтированная версия ресурса с той же контрольной суммой. Если есть, то повторно ресурс не монтируется.

После каждого обновления все неиспользованные распакованные ресурсы отмонтируются.


### Подсчет контрольных сумм

Контрольная сумма считается только по именам файлов и их содержимому. Два ресурса, которые являются файлами или папками и отличаются только метаданными (например, флаги исполняемости) или только пустыми папками, будут неотличимы для курьера. Пустые файлы влияют на контрольную сумму.

### Необязательные ресурсы

Некоторые ресурсы могут быть необязательными (`required: false`). Это означает, что такой ресурс может отсутствовать. Если такое произойдёт, то все workplace, в которых этот ресурс упоминается, будут удалены. Courier считает, что renderer для таких workplace умеет работать при отсутсвии всей папки.

## Адрес /admin

### /admin?action=stats

По этому адресу отдаются сигналы в формате unistat для [yasm](https://wiki.yandex-team.ru/golovan/). Сигналы:
* `unistat-courier-instances-count_ammm` - всегда отдаётся 1, используется для подсчёта количества запущенных courier'ов;
* `unistat-courier-last-update-delta_axxx` - время, прошедшее с последнего успешного обновления, мс. `n/a`, если процесс курьера не получал запросов на обновления. Учитывается любой запрос на обновление, даже такой, при котором ни одного ресурса не было изменено;
* `unistat-courier-update-prepare-workplaces-duration_ahhh` - время, ушедшее на подготовку ресурсов в рамках одного запроса, мс;
* `unistat-courier-update-workplaces-duration_ahhh` - время, ушедшее на перезапуск `renderer` во всех `workplaces` в рамках одного запроса, включая случайную задержку, создаваемую `restartDelayUpperBound`, мс;   
* `unistat-courier-no-actual-update_ammm` - количество раз, когда запрос на обновление не привёл к изменению ресурсов.

### /admin?action=is-ready

Возвращает ответ с кодом 200 с телом `true`, если курьер готов обрабатывать запросы на обновление. Возвращает ответ с кодом 503 и телом `false` в противном случае. Курьер становится готовым обрабатывать запросы после первичного обновления в рамках выполнения команды `watch`. 

## Структура папок
```
config[workingDir]
    |
     ---unpacked-resources – хранилище для распакованных ресурсов
    |       |
    |        ---<human readable dir name> – уникальная папка для ресурса
    |               |
    |                ---<hash sum> – конкретная версия одного ресурса
    |                       |
    |                        ---файлы из архива с ресурсом
     ---temp – папка для временных файлов
     ---service-state.json – контрольные суммы ресурсов, которые сейчас подготовлены в config[preparedResourcesDir]

config.workplaces[i].path – папка с подготовленными ресурсами для каждого из workplaces
    |
     ---<target> – симлинка на конкретную версию одного ресурса
    |
     ---<target> – симлинка на ресурс, который не нужно распаковывать
```

## Дебаг

Полный дебажный вывод включается переменными окружения `FS_DEBUG=1 DEBUG=*`.

## Обновление sandbox-ресурса с курьером

Подготовить зависимости (по инструкции из infratest):
Из папки infratest `pnpm run bootstrap -- --filter {packages/kotik}...`

Создать sandbox-ресурс:
Из папки renderer-courier `pnpm run upload`. Примерный вывод команды будет
```
> @yandex-int/renderer-courier@0.1.0 upload /home/slava-b/tmp/infratest/packages/renderer-courier
> npm run build && node ./build/bin/upload

> @yandex-int/renderer-courier@0.1.0 build /home/slava-b/tmp/infratest/packages/renderer-courier     
> tsc --build

Running `npm pack`
Extracting archive
Installing dependencies
Uploading resource to sandbox
Resource uploaded successfully: https://sandbox.yandex-team.ru/resource/1139215629/view
Don't forget to release task http://sandbox.yandex-team.ru/task/515915373/view
```

Sandbox-ресурс будет содержать архив с кодом курьера и всеми необходимыми `node_modules`.

Задачу, к которой привязан релиз, НУЖНО (в отличии от renderer) зарелизить (release в sandbox task) для отправки в прод

## Поддержка squashfs
Курьер умеет монтировать шаблоны, упакованный в образ squashfs, к этой функциональности предъявляются следующие требования:
* На хосте должна присутствовать утилита `portoctl` (работа с образами происходит через неё): https://github.com/yandex/porto/blob/master/porto.md
* `preparation` для ресурса должен быть следующим:
```json
{
    "type": "mount",
    "fsType": "squashfs"
}
```
* Перед запуском рендерера в секции рендерера необходимо вызывать `courier -c config.json waitingforsquashfs`, чтобы избежать запуска рендерера не дождавшись монтирования образов
