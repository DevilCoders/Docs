# cli

## Установка

1.  Устанавливаем пакет:

    ```bash
    npm i @lavka-js-toolbox/cli
    ```

1.  Создаем в корне проекта исполняемый файл `cli.js`:

    ```bash
    touch cli.js && chmod +x cli.js
    ```

1.  Настраиваем `cli.js`:

    ```js
    #!/usr/bin/env node
    const {Cli} = require('@lavka-js-toolbox/cli');
    void new Cli().run();
    ```

1.  Регистрируем файл в `package.json` (**my_app** &mdash; алиас исполняемого файла):

    ```
    "bin": {
      "my_app": "cli.js"
    }
    ```

1.  Применяем npm алиас команды:
    ```bash
    npm link
    ```

## cliOptions: `new Cli({...cliOptions})`

-   _string_ `baseDir`, _default_ `'src/cli'`, _env_: `JSTOOL_CLI_BASE_DIR` > `CLI_BASE_DIR`. Директория с командами.

-   _string_ `babelRegister`, _default_ `''`, _env_: `JSTOOL_CLI_BABEL_REGISTER` > `CLI_BABEL_REGISTER`. Путь к js файлу
    экспортирующему объект опций для [@babel/register](https://babeljs.io/docs/en/babel-register). Если не указан,
    то `@babel/register` не используется.

-   _string_ `commandSuffix`, _default_ `'-command'`, _env_: `JSTOOL_CLI_COMMAND_SUFFIX` > `CLI_COMMAND_SUFFIX`. Суффикс
    идентифицирующий файл, как команду.

-   _string_ `hooksPath`, _default_ `'hooks'`, _env_: `JSTOOL_CLI_HOOKS_FILE` > `CLI_HOOKS_FILE`. Имя файла с cli
    хуками.

## Использование

-   Название файла команды должно быть с суффиксом `cliOptions.commandSuffix` (например: `hello-command.ts`). Сам модуль
    должен экспортировать объект `usage` и метод `handle`.

-   Команды можно раскладывать по директориям, при вызове каждая директория указывается через пробел. Например:

    ```bash
    # Для команды "<cliOptions.baseDir>/service/db/migrate-command.ts"
    my_app service db migrate
    ```

-   [Пример команды](example/example-command.ts)

-   О других возможностях `usage`:

    -   [ts-command-line-args](https://github.com/Roaders/ts-command-line-args#usage-guide)
    -   [command-line-args](https://github.com/75lb/command-line-args#synopsis)

-   При выполнении команды доступен глобальный метод [cliRuntime()](src/types.ts)

-   Вывести справку по доступным командам:
    ```bash
    my_app -h
    ```

## Хуки

Для команд можно задать хуки. Для этого нужно создать файл `hooks.ts` (опция `cliOptions.hooksPath`) в
директории `src/cli/` (опция `cliOptions.baseDir`). Чтобы использовать хук, надо экспортировать из файла метод с
названием хука.

-   `beforeCommand`
-   `onCommandSuccess`
-   `onCommandFailure`

[Пример файла с хуками](example/hooks.ts)
