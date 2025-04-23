# Debug дев-сервера

Чтобы дебажить дев сервер на удаленной машине потребуется:

1. Включить inline-source-map в .env.development: SERVER_SOURCE_MAP,
   пример есть в env.development.example. Внимание: source-map замедляет сборку. Внимание: наш rsync скрипт не следит за изменениями env.development, потребуется перезапустить rsync.
2. Открыть ssh соединение с пробросом локального порта 9221
   на порт удаленной машины 9229:

```
ssh -L 9221:localhost:9229 [login].ui.yandex.ru
```

3. Запустить дев сервер на удаленной машине
   (в этом npm скрипте уже есть флаг --inspect):

```
npm run dev:inspect
```

4. Присоединиться с помощью своего любимого дебаг-клиента.

    Для WS.
    Нужно добавить конфигурацию:
    Run -> Edit configurations... -> Attach to Node.js/Chrome -> + -> Name: your name, Host: localhost, Port: 9221 -> Ok
    И можно подключаться через иконку жука или хоткей ^D

5. Можно ставить breakpoints и дебажить api или SSR

Более подробно [о дебаге nodejs](https://nodejs.org/de/docs/guides/debugging-getting-started/) .
