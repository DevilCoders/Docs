# Разработка на логрусах

* [Старая инструкция находится тут](https://wiki.yandex-team.ru/market/frontend/dev-environment/)
* С проблемами приходите в [Market Front Infra Support](https://t.me/joinchat/C5yyIUy9ythghPB6TfsD7w)


Разработка приложения происходит на удалённых серверах, они именуются логрусами. На них используется svn.

Список логрусов:
```bash
market.logrus01vd.yandex.ru
market.logrus02vd.yandex.ru
market.logrus01hd.yandex.ru
market.logrus01ed.yandex.ru
```

Как понять, какой подходит тебе? ~~Он захочет тебя убить.~~
Ты можешь выбрать любой из них. Развертывание рабочей копии осуществляется там же с помощью специального скрипта.

{% note tip %}

Узнать о самочувствии логрусов можно через [Wall-e](https://wall-e.yandex-team.ru/projects/hosts?fqdn=logrus)

{% endnote %}

## Настройка доступов

1. Сгенерируй ssh-ключ для авторизации внутри сети
([MacOs](https://wiki.yandex-team.ru/security/ssh/macos) | [Windows (+ Putty)](https://wiki.yandex-team.ru/security/ssh/windows), [Linux](https://wiki.yandex-team.ru/security/ssh/linux))
2. Скопируй текстом публичный ключ и загрузи его на [Staff](https://staff.yandex-team.ru)
![SSH на Staff](_assets/logrus/staff_ssh.png)
После этого ключ сам прорастёт на те машины, на которые ты можешь ходить по SSH. Это занимает некоторое время, но в течение дня он должен разъехаться.
3. Настроить SSH Agent Forwarding. Это позволит проксировать авторизацию ключами при работе на удаленных хостах.
    * Нужно создать в папке `~/.ssh`  файл config, и указать там хосты, куда нужно форвардить
        ```bash
        Host market.logrus*
          ForwardAgent yes
        ```
   * Чтобы не добавлять ключ каждый раз руками, можно в `.bashrc`  (или `.profile`  – зависит от того, какая у тебя ОС) вписать автоматическое добавление ключа при старте терминала: `ssh-add <путь до ключа>`.
     После выполнения этой команды SSH-соединения из этого терминала получат форвардинг на подходящие под настройки хосты.

{% note tip %}

Ключ обычно лежит в файле `~/.ssh/id_rsa`. Публичный ключ в `~/.ssh/id_rsa.pub`.

{% endnote %}

## Развёртывание рабочей копии

1. Зайди по SSH на один из логрусов (`ssh market.logrus0**d.yandex.ru`, добавь `-A` если не настроен SSH Agent Forwarding). Если при подключении тебе выдаётся ошибка `Host key verification failed`, попробуй удалить `~/.ssh/known_hosts`.

    {% note tip %}

    Полезное ПО для комфортного подключения по SSH:
    * Mosh - не разрывает ssh-соединения при отключении от интернета/ухода компьютера в сон
    * Tmux - добавляет скролл и сохраняет сессии на серверах

    {% endnote %}

2. При первом заходе на логрус будет предложено установить `nvm` (Node Version Manager)
3. Текущая версия NodeJS `16`. Нужно выполнить `nvm install 16.9.1`, `nvm alias default 16.9.1`  и `nvm use 16.9.1`.
4. Текущая версия npm `6.13`. Теперь необходимо обновить npm: выполни `npm i -g npm@6.13`.
5. Убедись с помощью `npm -v` и `node -v` что стоят корректные версии NodeJS и npm.
6. Установи [Veendor](https://github.com/mutantcornholio/veendor) `npm i -g veendor`. Он кэширует `node_modules` и позволяет быстрее устанавливать зависимости.
7. Установи [Carrier](https://github.yandex-team.ru/market/carrier) `npm i -g @yandex-market/carrier --registry=http://npm.yandex-team.ru`. Он ещё интегрируется и планируется, что заменит veendor.
8. Теперь необходимо выполнить команду `make_wc` для развёртывания проекта. (При проблемах с разворачиванием проекта данной утилитой, выполни команду `ssh-add -l` и попробуй ещё раз)
    * Потребуется выбрать проект `marketfront` - объединенный репозиторий десктопа, тача и фапи Маркета. (Без визарда можно запустить командой `make_wc -p marketfront`)
    * Появится предложение о запуске установки зависимостей проекта.
    * При завершии установки ты увидишь довольно полезную информацию **обрати на неё особое внимание**:
      * `project copy is deployed to <path>` - фактическое местонахождение твоего проекта на сервере
      * `created symlink <folder-name> in your home directory` - симлинк на твой проект в домашней папке
      * `work copy URL` - адреса десктопа, тача и fapi, по которым ты сможешь сходить в приложение, после его запуска.

    {% note warning %}

    * `make_wc` при повторном выполнении перезапишет существующий проект
    * Если ты захочешь удалить рабочую копию с сервера, то недостаточно будет выполнить в домашней директории `rm -rf <folder>`, т.к. ты удалишь симлинк. Необходимо удалить фактическую директорию твоего проекта `/var/lib/yandex/marketfront/<login>`

    {% endnote %}

9. У фронта маркета есть три платформы:
    * `marketfront_<login>/market/platform.desktop` - веб версия для десктопа
    * `marketfront_<login>/market/platform.touch` - веб версия для тача
    * `marketfront_<login>/api` - FAPI (API для мобильных приложений)

10. Для сборки проекта используй команду `npm run make:all` в одной из платформ (Не нужно, если сделал постустановку в `make_wc`).
11. Для запуска сборки бандлов и серверного кода в watch режиме, используй `npm run webpack:watch`.
12. Для запуска сервера используй `npm run start`. `npm run start:debug` запустит сервер с дебаггером.

    {% note warning %}

    * `npm run webpack:watch` и `npm run start` следует запускать в разных окнах.
    * `npm run webpack:watch` собирает только "основные страницы" приложения. Добавить свои страницы можно через параметр `PAGES`. Пример: `PAGES=IndexPage,CartPage npm run webpack:watch`
    * Для запуска вотчера всех страниц используй `npm run webpack:watch:hard`. Но данный процесс длится заметно дольше.

    {% endnote %}

13. Теперь проект должен быть доступен по адресу вида:
    `https://<working-copy-name>.<platform-name>.<host>.<project-name>.yandex.ru`, где
    * `<working-copy-name>`  - имя рабочей копии, совпадает с логином
    * `<platform-name>`  - desktop/touch/api
    * `<host>`  - logrus01vd/logrus02vd/logrus01hd/logrus01ed
    * `<project-name>`  - имя проекта (market)

## Развертывание проекта marketfront
Существует 2 варианта разворачивания проекта (разными VCS), и как следствие - моделей/вариантов его дальнейшего сопровождения:
- [{#T}](./svn.md)
- [{#T}](./git-shards.md)

## Настройка синхронизации файлов

Концепция заключается в том, чтобы разрабатывать код локально, в удобной IDE и синхронизировать его с развернутой ранее удаленной рабочей копией проекта. Для этого можно воспользоваться передачей данных через SFTP (*rsync работает плохо*).

Прежде всего, необходимо склонировать на локальную машину нужный проект.

Однако прежде нужно выполнить те же шаги, что и на удаленной машине:

* Требуется нода версии `16`, поэтому следует установить `nvm`.
* Затем переключи версию: `nvm use 16.9.1 || nvm install 16.9.1`.
* И установи глобально нужную версию npm - для этого выполни `npm i -g npm@6.13`
* Следом установи veendor - `npm i -g veendor`
* Всё, теперь осталось установить проектные зависимости, выполни только `npm run bootstrap` и `npm run configure`.

{% note tip %}

Есть рекомендация добавить в `~/.bash_profile` следующий код, для подхвата зависимостей в проекте:
```bash
export PATH="./node_modules/.bin:$PATH"
```

{% endnote %}

{% list tabs %}

- Webstorm

    1. Пункт меню `Help -> Edit custom VM options`. IPv4 поменять на IPv6:
        ```bash
        ...
        # -Djava.net.preferIPv4Stack=true
        -Djava.net.preferIPv6Stack=true
        ...
        ```
    2. Открыть нужный проект (предполагается, что исходники уже склонированы) и зайти в `Tools  -> Deployment  -> Configuration`.
    3. Нажать кнопку добавления новой конфигурации и указать имя (например, имя хоста, на котором развернута рабочая копия).
    Тип поменять на SFTP, после чего указать хост, логин, путь к файлу ключа и passphrase, если есть.
        ![SFTP в Webstorm 1](_assets/logrus/logrus_webstorm_sftp_1.jpg)
        ![SFTP в Webstorm 2](_assets/logrus/logrus_webstorm_sftp_2.jpg)
        ![SFTP в Webstorm 3](_assets/logrus/logrus_webstorm_sftp_3.jpg)
    4. По нажатию кнопки `Test SFTP Connection`  должно показаться уведомление о новом сертификате (его следует принять) и, если всё сделано верно, увидеть сообщение об успехе. Если подключиться не удалось, убедитесь, что вы правильно сделали первый шаг (IPv6) и перезагрузили IDE.
    5. На закладке `Mappings ` следует указать `Deployment Path` — тот самый, что выдавал `make_wc`, и на который созданы симлинки
    6. Чтобы файлы удалялись на Remote при удалении локально (скорее всего, вам это нужно), нужно поставить галочку Delete remote files when local are deleted в `Tools -> Deployment -> Options`

- VS Code

    Имеет смысл поставить расширение для Flow: [Flow Language Support](https://marketplace.visualstudio.com/items?itemName=flowtype.flow-for-vscode)

    1. Открыть менеджер плагинов
    2. Найти и установить `liximomo.sftp`
    3. После перезагрузки вызвать `cmd+shift+p -> SFTP:config`
    4. Открыть созданный `sftp.json` конфиг в папке `.vscode` в корне проекта
    5. Cкопировать туда этот конфиг, заменяя нужные пути или написать свой конфиг с нуля. Пример конфига:
        ```bash
        {
            "host": "market.logrus01ed.yandex.ru",
            "port": 22,
            "username": "<username>",
            "protocol": "sftp",
            "privateKeyPath": "/Users/<username>/.ssh/id_rsa",
            "passive": false,
            "interactiveAuth": false,
            "remotePath": "/home/<username>/node.redmarket_<hostname>/",
            "uploadOnSave": true,
            "syncMode": "update",
            "watcher": {
                "files": "*",
                "autoUpload": true,
                "autoDelete": true
            },
            "ignore": [
                "/.vscode/",
                "/.git/",
                "/.DS_Store",
                "/node_modules/**"
            ]
        }
        ```
    6. `cmd+shift+P -> SFTP: Sync to Remote`
    7. Остальные команды можно посмотреть в доке плагина

{% endlist %}

## Инструменты

[Генератор базовых сущностей (entity, резолвер, ресурс, FAPI-хэндлер, виджет)](https://wiki.yandex-team.ru/market/frontend/tools/generator-market/)

## Отладка проекта

{% list tabs %}

- DevTools for Node

    **Только для Chromium**
    1. Убеждаешься, что `vhost.txt`  есть (./platform.desktop), и в нем лежит имя твоего хоста (bykhovtsev.desktop.logrus01vd.market.yandex.ru)
    2. Открываешь хром в инкогнито, жмешь f12 (cmd+shift+i) и переходишь по выделенному
    3. Там находишь app.js слева, тыкаешь, наблюдаешь приход старости, дебажешь. После обновления кода, повторить (он там кнопку reconnect предложит)

- Firefox Debugger

    * [Firefox Developer Edition](https://www.mozilla.org/ru/firefox/developer/)
    * [Интерактивный Playground (в стиле Mozilla)](https://mozilladevelopers.github.io/playground/debugger/)
    * Аналогом `chrome://inspect` служит `about:debugging`, [подробнее на MDN](https://developer.mozilla.org/en-US/docs/Tools/about:debugging).
    * [Актуальная инструкция по линковке WebStorm и Firefox в доках Jetbrains](https://www.jetbrains.com/help/webstorm/debugging-javascript-in-firefox.html).

- Webstorm

    [Можно почитать подробнее здесь](https://wiki.yandex-team.ru/market/verstka/platform/dev-env/#nastrojjkaudaljonnojjotladkivwebstorm/phpstorm/idea)

- VSCode

    Удалённая отладка VSCode описана [тут](https://code.visualstudio.com/docs/nodejs/nodejs-debugging#_remote-debugging)

    В целом всё сводится к созданию файла `.vscode/launch.json`  в корне репозитория:
    ```bash
    {
        "version": "0.2.0",
        "configurations": [
            {
                "type": "node",
                "request": "attach",
                "name": "Attach to Remote",
                "address": "market.logrus01vd.yandex.ru",                       // Замени на имя машины
                "port": 1778,                                                   // Замени на порт для отладки (полученный выше)
                "localRoot": "${workspaceFolder}",
                "remoteRoot": "/home/gerichhome/node.marketplace_gerichhome1",  // Где на удалённой машине развёрнута рабочая копия
                "protocol": "inspector",
                "sourceMapPathOverrides": {
                    "webpack:///../node_modules/*": "${workspaceRoot}/node_modules/*",
                    "webpack:///./*": "${workspaceRoot}/platform.desktop/*",    // Если используется другая платформа - замени desktop на нужное
                    "webpack:///../src/*": "${workspaceRoot}/src/*",
                    "webpack:///*": "*"
                },
                "sourceMaps": true
            },
        ]
    }
    ```
    Затем нажимаем `Ctrl+Shift+D` и запускаемся.
    Можно отлаживаться, ставить бряки в исходниках, смотреть переменные.

{% endlist %}

## Если у вас mac на m1

[Настройка flow на m1](https://wiki.yandex-team.ru/market/frontend/dev-environment/flow-m1/)

