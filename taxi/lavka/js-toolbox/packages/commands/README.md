# commands

Пакет для запуска простых npm команд.

Типовой пример использования — это _npm run_ фасады:

```json
{
    "scripts": {
        "lint": "commands/run.js ./lint",
        "compile": "commands/run.js ./compile",
        "dev:install": "commands/run.js ./dev/install"
    }
}
```

Код команд пишется на _TypeScript_ и компилируется в рантайме через _ts-node_.

Файл команды должен экспортировать метод **default**, либо **run**.

---

## Быстрый старт

Ставим пакет:

```bash
npm i -D @lavka-js-toolbox/commands
```

Создаем папку `commands/` и **run.js** точку входа:

```bash
mkdir commands
echo "#!/usr/bin/env node" > commands/run.js
chmod +x commands/run.js
```

Настраиваем **run.js**:

```js
#!/usr/bin/env node

require('@lavka-js-toolbox/commands/dist/run')
    // Настраиваем ts-node/register на свой вкус
    // Подробности: https://www.npmjs.com/package/ts-node#programmatic
    .tsNodeRegister({
        transpileOnly: true,
        require: ['tsconfig-paths/register'],
        compilerOptions: {
            module: 'commonjs'
        }
    })
    .run({commandsDir: __dirname}); // указываем корневую папку для команд
```

Создаем команду (например, `commands/hello.ts`):

```ts
// может быть `async`
export default () => {
    console.log('Hello!');
};
```

И добавляем команду в _package.json_:

```json
{
    "scripts": {
        "hello": "commands/run.js ./hello"
    }
}
```

Теперь скрипт можно запустить через _npm run_:

```bash
npm run hello
```
