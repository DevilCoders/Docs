# Surfwax browser runner

Сервис, который запускает браузеры для surfwax. На данный момент поддержаны браузеры: `safari13`, `safari15`.

## Конфиг

Пример конфигурации для запуска safari13:

**runnerBinPath** - в данном случае, runnerBinPath - бинарный файл appium-а, который запустит браузер. В случае с браузерами, которые запускаются в контейнере, это должен быть путь к docker runnerBinPath
**platform** - платформа, на которой будет запущен браузер. На данный момент доступны платформы: `ios`.

```js
{
    "safari": {
        "versions": {
            "13.0": {
                "runnerBinPath": "./node_modules/.bin/appium", //
                "platform": "ios" // Для каждой платформы своя реализация раннера. На данный момент доступны платформы: `ios`
            }
        }
    }
}

```

## HTTP API v0

### `POST /api/v0/browser`
Стартует браузер с укзанными параметрами:

Body:
```
{
    browserName: 'safari';
    browserVersion: '13.0';
    port: 4321;
}
```

Возможные статусы: 200, 429, 500.

### `DELETE /api/v0/browser`

Завршает браузер с указанными параметрами.

Body:
```
{
    browserName: 'safari';
    browserVersion: '13.0';
    port: 4321;
}
```


Возможные статусы: 200, 500.

## Разработка
```
npm i
npm run build
DEBUG=surfwax-browser-runner* node build/index.js --port 4433 --config ./runner-config.json --limit 5
```

## Выпуск версии
```
npm version <patch/minor/major>
npm run build && npm publish --registry=http://npm.yandex-team.ru
```
