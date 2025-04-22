# ❗ Strict TS
На проекте не активирован глобально strict режим, поэтому в начале разработки нового функционала необходимо активировать его для новых фич.

_./client/tsconfig.json_
```
{
  "compilerOptions": {
    "typeRoots": ["../node_modules/@types", "./@types"],
    "plugins": [
      {
        "name": "typescript-strict-plugin",
        "paths": [
          "./@types/global.d.ts",
          //добавляем сюда путь до новой фичи
          "./feautures/organizations"
        ]
      }
    ]
  }
}

```

Есть возможность включить для одного файла
```
// @ts-strict

const func = (param: string) =>{
  // blablabla
}

```
Подробнее тут https://github.com/allegro/typescript-strict-plugin

# Как начать разработку

Нужно завести себе собственную разработческую витруалку в [QYP](https://qyp.yandex-team.ru),
разработка ведётся только оттуда по причине наличия зависимостей от сетевых правил файрвола
и грантов для системы авторизации.
Если у вас уже есть почтовая дев-машина, можно вести разработку прямо на ней.
Для того, чтобы всё работало корректно и с нужными доступами, нужно также состоять
[в группе ABC](https://abc.yandex-team.ru/services/sarah/).

[Инструкция по заведению виртуалки](../../../../tools/qyp#инструкция)

Локально стоит также запустить `npm ci` в корне монорепозитория,
чтобы начали работать гит-хуки (`pre-commit`, например, описаны в секции `husky`
в корневом проектном [package.json](../../package.json)).

## Запуск проекта

1. Подготовить окружение (ставит зависимости + секреты)
```shell script
cd ~/arcadia/yandex360/frontend/services/sarah
npm run prepare-dev
```
2. Запустить проект
```shell script
npm start

# Можно указать параметр SOURCE_MAP_TYPE=<тип-source-map> для сборки с source maps
SOURCE_MAP_TYPE=none npm start
#
SOURCE_MAP_TYPE=eval npm start
```
3. Для получения ссылки в браузере нужно выполнить `npm run url`. Открыть в браузере `https://<vm_name>-arc.
sarah-dev.mail.yandex.ru/`, где `<vm_name>` - название виртуальной машины в QYP.


## Полезные советы

В настройках плагина для автоматической синхронизации необходимо добавить в игнор следующие директории/файлы:

- `node.sock`;
- `webpack.sock`
- `server/node_modules`.

Помогает держать проект запущенным на постоянной основе (например, для поднятия стенда для фичи) и не зависеть от ssh-сессии.

```shell script
screen -S <name>
npm start
```

```shell script
# Создание сессии:
screen -S <name>
# где <name> - любое имя

# Посмотреть список сессий:
screen -ls

# Возврат к сессии:
screen -r <name>
```

Иногда для дебага серверного кода помогает включить debug-режим в Даффмане, в котором он начинает писать в консоль примерно всё:
```shell script
DEBUG=core:* npm start
```

### Разработка в VSCode

Для разработки в VSCode подойдёт плагин `sync-rsync`.
Примерный конфиг:
```json
{
  "sync-rsync.args": [
    "--delete",
    "--force"
  ],
  "sync-rsync.autoHideOutput": true,
  "sync-rsync.autoShowOutputOnError": false,
  "sync-rsync.exclude": [
    ".git",
    ".vscode",
    "node.sock",
    "webpack.sock",
    "server/node_modules",
    "dist"
  ],
  "sync-rsync.flags": "vza",
  "sync-rsync.remote": "<username>@<host>:~<path>",
  "sync-rsync.shell": "ssh",
  "sync-rsync.watchGlobs": [
    "server/**/*",
    "client/**/*"
  ],
  "debug.node.autoAttach": "off"
}
```

Можно также использовать SFTP (liximomo.sftp).
Примерный конфиг:
```json
{
    "protocol": "sftp",
    "port": 22,
    "username": "YOUR_USERNAME",
    "remotePath": "/home/YOUR_HOME_FOLDER/frontend",
    "privateKeyPath": "~/.ssh/id_rsa",
    "uploadOnSave": true,
    "profiles": {
        "qyp": {
            "host": "QYP_HOST"
        }
    },
    "defaultProfile": "qyp"
}
```

### Разработка в WebStorm

Настройка встроенной возможности синка по sftp весьма тривиальна, делается через
`Tools` => `Deployment` => `Configuration`.

Для автодеплоя по sftp нужно включить предпочтение ipv6 в WebStorm (`Cmd` + `Shift` + `A` => `Edit Custom VM Options`)
```
-Djava.net.preferIPv4Stack=false
-Djava.net.preferIPv6Addresses=true
```
