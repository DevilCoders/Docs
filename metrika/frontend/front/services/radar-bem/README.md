Начало разработки
---------------

Заходим на дев машинку:

    ssh -A metrika-dev.haze.yandex.ru

где <user> и <app> необходимо заменить на свой логин и имя проекта соответственно.
В <app> должны содержаться только буквы, цифры и `-`

Дальнейшая сборка и запуск автоматизированы в одном скрипте:

    cd /home/<user>/www/<app>
    make prebuild // достаточно запустить один раз, для установки зависимостей и правильной линковки конфигов
    make cleanwatch // будет следить за изменениями файлов, перезапускать node.js и пересобирать стили/клинетский js

Сайт будет доступен по адресу `<app>-<user>.radar.dev.metrika.yandex`

Разработка
---------------

Разработка ведется по слегка модифицированному [git-flow](https://wiki.yandex-team.ru/users/rodik/git-flow)

Исходники для текущей версии продакшена лежат в ветке master, а для разработки используется ветка develop

На проекте используется:

 * [bem-node](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fbem-node) - node.js + BEM = SPA
 * [Vow](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fdfilatov%2Fvow%2Ftree%2F0.3.x) версии 0.3. Поставляется вместе с `bem-node`
 * [bem-node-yandex](https://github.yandex-team.ru/bem-node/bem-node-yandex) - внутренние уровни переопределения для Яндекса
 * [islands](https://lego.yandex-team.ru/libs/islands/v5.8.1/) - библиотека блоков
 * [promised-models](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fpromised-models) - модели
 * [bem-promised-models](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fbem-promised-models) - обертка над моделями в терминах BEM
 * [bem-json](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem-node%2Fbem-json) - шаблонизатор, результат которого скармливается в [bemhtml](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fbem%2Fbem-xjst%2Ftree%2Fv7.x) для получения финальной строки html
 * [gulp](https://h.yandex-team.ru/?http%3A%2F%2Fgulpjs.com) и [enb](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fenb%2Fenb) - для сборки
 * [babel](https://h.yandex-team.ru/?https%3A%2F%2Fbabeljs.io) с [preset-es2015](https://h.yandex-team.ru/?https%3A%2F%2Fbabeljs.io%2Fdocs%2Fplugins%2Fpreset-es2015%2F) - для использования es6 синтаксиса на клиенте
 * [es6-shim](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fes-shims%2Fes6-shim) - полифиллы из es6 для использования на клиенте

Сборка умеет автоматически инлайнить картинки - необходимо добавить параметр `inline_image` в `url`. Например:

    background-image: url('icon.png?inline_image=1');

При сборке пакета такая иконка будет заинлайнена, а для `svg` еще и запущен `svgo`. При разработке этого не происходит.

Forever
---------------
Свою бету можно демонизировать, чтобы, например, она всегда была доступна. Для этого:

    make build
    make forever-start

Чтобы применить к ней изменения:

    git pull // или другим образом поменять файлы
    make rebuild // или build, если обновились зависимости в package.json
    make forever-restart

Для останова - `make forever-stop`

Структура проекта
---------------
 * `autobuild_blocks` сгенерированные данные для других блоков, например список выходных дней. автогенерируется

структура `blocks/`

 * `blocks/api` блоки, которые предоставляют интерфейс на получение данных из внешних источников (бекенда)
 * `blocks/common` блоки, не имеющие DOM-представления, обычно всякие helper-блоки
 * `blocks/data` блоки, специально для получения данных их API (используя ctx.defer())
 * `blocks/desktop` основые блоки, внутри обычно шаблоны, css и браузерная js-часть
 * `blocks/external` подключение внешних библиотек в бэм-сборку
 * `blocks/inherits` расширение внешних блоков и библиотек
 * `blocks/models` модели
 * `blocks/pages` контроллеры страниц

Сборка релизов
---------------
Полезная информация по флоу находится тут - https://wiki.yandex-team.ru/users/antonkot/test-flow/. В статье речь идёт о Метрике, но все или почти все применимо к Радару.
Часть действий при сборке релиза автоматизировано с помощью Jenkins. Действия примерно следующие:
1) Заходим в https://jenkins.metriqa.yandex.ru/view/Radar/job/radar-release/;
2) Жмём `Build with parameters`;
3) Указываем новую версию. Текущую можно посмотреть на проде по урлу https://radar.metrika.yandex/version. Например, на проде сейчас версия `1.8.4`, значит в Jenkins'e в поле ввода новой версии нужно написать `1.9`;
4) Ждем завершения джобы - должна создасться релизная ветка на гитхабе, релизный тикет в стартреке, к нему привязаться все задачи, которые попали в релиз. В кондукторе появятся два тикета - на ноду и статику. Ждем пока они выкатятся и отдаем в тестирование.

Если в процессе тестирования были найдены баги, то делаем ПР в релизную ветку, ждем бета-тестирования, мержим и пересобираем в Jenkins. Для удобства можно нажать `Rebuild Last`, чтобы не забивать номер релиза вручную. Jenkins сам определит что релиз с такой версией существует и не будет создавать новую ветку и тикет, а допишет все в текущие.

Дополнительные команды
---------------

Мы используем специальные версии node.js, у которых жестко зафиксированы пути до бинарников. Например у пакета `nodejs-6` он такой:

    /opt/nodejs/6/bin/node
    /opt/nodejs/6/bin/npm

При локальной разработке некоторые из команд удобно запускать локально. Чтобы не создавать указанные выше пути, необходимо выставить переменную окружения `TRAFFIC_LOCAL=1`. Тогда пути до бинарников node и npm будут взяты из глобального PATH.

Сборка нового проекта (внутри вызов `make build`):

    make

Сборка (установка npm зависимостей и вызов `make rebuild`)

    make build

Пересборка (обновление праздников и собственно пересборка проекта)

    make rebuild

Слежение за изменением файлов. Нужно запускать после `make build`/`make rebuild`, т.е. файлы уже должны быть на файловой системе. При изменении common.js и priv.js файлов сервер рестартует (используется nodemon). deps.js файлы не отслеживаются. Добавление/удаление файлов не отслеживается. Из-за особенностей кеширование в gulp первые сборки после запуска будут долгими

    make watch

Слежение за изменением файлов. Под капотом запускает `make clean` и `make build`. первые пересборки после запуска этой команды будут быстрыми. В остальном аналогична команде `make watch`

    make cleanwatch

Чистая сборка. Удаляет node_modules (см. `make depsclean`), а так же кеш `enb` и уже сгенерированные предыдущей сборкой файлы (см. `make clean`)

    make cleanbuild

Обновление переводов. В качестве параметра можно передать имя блока/блоков (именно имя, а не путь), чтобы не скачивать все переводы

    make i18n.get [blocks=block1,block2]

Список праздничных дней

    make holidays.get

Удаление пакетных зависимостей. Чистит кеш у npm, а так же удаляет node_modules

    make depsclean

Линк конфигов. В зависимости от переменной окружения `YENV` сделать из `./node_modules/configs` симлинк к нужной папке в `./configs/`

    make configs

Удаления кеша у `enb` и уже собранных файлов

    make clean

Установка зависимостей

    make deps

Проверка кода по всему проекту с помощью `eslint`

    npm run lint

Проверка кода по всему проекту и исправление ошибок. Вызов [eslint ./ --fix](https://h.yandex-team.ru/?http%3A%2F%2Feslint.org%2Fdocs%2Fuser-guide%2Fcommand-line-interface%23options)

    npm run lint -- --fix

Некоторые сведения по общим зависимостям
---------------

 * [nodejs-6](https://wiki.yandex-team.ru/Lego/nodejs/packages)
 * [Версии пакетов Node.js, биндингов и общих бибилиотек](https://wiki.yandex-team.ru/ui/frontend/consortium/nodejs/versionsboard)
 * [Geobase5](https://wiki.yandex-team.ru/libgeobase/TranslocalMigration)
