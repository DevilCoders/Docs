# Как разрабатывать Тесткоп?

## Как запустить приложение?

Чтобы запустить приложение, выполните следующую команду:

```
npm run develop
```

Сборка клиентского кода происходит с использованием `webpack`, поэтому необходимо запустить процесс слежения за изменениями и пересборки клиентского кода в отдельной вкладке:

```
npm run watch
```

## Как запустить unit-тесты и линтеры?

Чтобы запустить unit-тесты и линтеры, выполните следующую команду:

```
npm test
```

Для запуска только линтеров:

```
npm run lint
```

## Как безопасно протестировать Testcop?

Чтобы не заскипывались тесты в конвейере и не заводились тикеты в проектных очередях.

1. Идем в глобальный Sandbox и находим какую-нибудь задачу запуска тестов, например [такую](https://sandbox.yandex-team.ru/task/359044708).

2. Открываем задачу (именно запуска тестов, не перепутайте с мастер-таской) и переходим во вкладку `Resources`.

3. Находим json-отчет – ресурс вида `инструмент-платформа.json`, например, `hermione-desktop.json` и копируем его ID.

4. [Разворачиваем локальный Sandbox](https://github.yandex-team.ru/search-interfaces/local-sandbox) и переходим на него по `ssh`.

5. Выполняем команду `cd /home/ваш логин/sandbox && ./sandbox add_resource -f --id ID-json-отчета`

6. После добавления ресурса в локальном Sandbox должна появиться задача с запуском тестов, копируем её ID (например, 21).

7. Запускаем dev-версию Testcop: `SANDBOX_HOST=http://seek-interface-dev9.search.yandex.net:3000 CLICKHOUSE_PASSWORD=password npm run develop` 
(хост заменяем на адрес вашего локального Sandbox, 3000 – на номер порта, на котором он развернут, а password нужно взять в [секретнице](https://yav.yandex-team.ru/secret/sec-01dbyvy4fec836rc5h9bqca5x9/)).

8. Открываем Testcop с номером задачи из локального Sandbox, например `open http://localhost:3000/task/21`.

9. Выбираем какие-либо тесты, скипаем или мьютим их, нажимаем `Submit`.

10. В появившемся модальном окне выбираем `Issue exists` и указываем какой-нибудь фейковый тикет так, чтобы регулярка пропустила его, например: `https://st.yandex-team.ru/ITSFAKE-123`. Если нужно все-таки убедиться, что тесткоп корректно создает тикет, то выбираем в модальном окне `Create issue`, задаем тикет в очереди `FEI`, смотрим результат и после этого закрываем тикет.

11. Идем в локальный Sandbox, находим там выполняющуюся таску `SANDBOX_CI_BUILD_SKIP_TESTS_LIST` и дожидаемся её успешного завершения.

12. Заходим во вкладку `Resources` и убеждаемся, что списки с заскипами созданы корректно. 

13. При этом история заскипов сохраняется не в production-базу `testcop`, а в `testcop_dev`. Содержимое dev-версии базы as is можно посмотреть на [дашборде](https://dash.yandex-team.ru/aqjfi03aond08) внизу (см. таблицу `testcop. dev`). Примечание: обе базы данных – `testcop` & `testcop_dev` – находятся [здесь](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-clickhouse/cluster/mdbt40ae21bh8kq7dgmr?section=databases).

## Как отлаживать приложение (клиент + сервер)?

### VS Code

Порядок действий:

- устанавливаем плагин для VSCode - [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) и браузер Chrome (с хромиумом у меня данный плагин не завелся)

- создаем конфигурационный файл `.vscode/launch.json` для дебага со следующим содержимым:

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "type": "node",
                "request": "launch",
                "name": "Server",
                "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/babel-node",
                "program": "${workspaceFolder}/server.js",
                "sourceMaps": true,
                "console": "integratedTerminal",
                "internalConsoleOptions": "neverOpen",
                "env": {
                    "NODE_ENV": "development"
                },
                "cwd": "${workspaceFolder}"
            },
            {
                "type": "chrome",
                "request": "launch",
                "name": "Client",
                "url": "http://localhost:3000",
                "webRoot": "${workspaceFolder}/client",
                "sourceMaps": true
            }
        ],
        "compounds": [
            {
                "name": "Testcop server + client",
                "configurations": ["Server", "Client"]
            }
        ]
    }
    ```

- запускаем наш webpack-dev-server командой `npm run watch`;

- ставим необходимые брейкпоинты в клиентском и серверном коде;

- запускаем дебаг с помощью комбинации клавиш `Fn + F5` и радуемся жизни.
