# Node.js Hello Tasklet

Выводит `Hello world!` в лог.

## Разработка

### Сборка кода

```console
$ nvm use
$ npm ci
$ npm run build
$ npm run dist

./dist/node_hello-macos
# Hello world!
```

### Сборка тасклета

```
ya tool tasklet build upload --build-schema ./dist/node_hello-linux
ya tool tasklet label move dev --to ${build_id}
ya tool tasklet run dev dummy_input.json -i json
```
