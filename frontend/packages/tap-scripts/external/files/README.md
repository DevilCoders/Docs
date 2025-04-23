# @yandex/tap-scripts

Форк [настроек и скриптов](https://github.com/marcopeg/create-react-app/tree/master/packages/react-scripts) от Create React App, предназначенный для сборки [tap-сервисов](https://yandex.ru/dev/turboapps/doc/concepts/index-docpage/).

## Установка

```bash
npm install --save git+ssh://github.com/yandex/tap-scripts#v0.1.2
```

## Документация

В `tap-scripts` доступны все возможности [Create React App](https://create-react-app.dev/docs/getting-started), за исключением перечисленных ниже отличий.

## Отличия от react-scripts

- Отключено создание vendor-чанков при сборке приложения
- Добавлен флаг `ignoreOrder: true` в плагине `MiniCssExtractPlugin`
- Возможность указать входную точку приложения:
    ```bash
    tap-scripts start ./path/to/index.js
    tap-scripts build ./path/to/index.js
    ```
- Возможность отключить eslint через переменную окружения `DISABLE_ESLINT=true`
- Возможность настроить тип source maps через переменную окружения `SOURCEMAP_TYPE=source-map`
