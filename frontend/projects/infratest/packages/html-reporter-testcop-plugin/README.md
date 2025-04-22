# html-reporter-testcop-plugin

Плагин для [html-reporter](https://github.com/gemini-testing/html-reporter), отображающий статистику из [testcop](https://testcop.si.yandex-team.ru).

## Установка

```sh
npm i @yandex-int/html-reporter-testcop-plugin --registry=http://npm.yandex-team.ru
```

## Компоненты

### SuccessRate

Компонент отображает **Success rate** для каждого теста.

#### Параметры

- `project: string` – название проекта (обязательный).
 
- `tool: string` – инструмент (обязательный).

Для работы плагина необходимо указать главную ветку _(branch)_ проекта в [конфиге](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/testcop-config/index.js) testcop.

```js
web4: {
    git: {
        owner: 'serp',
        repo: 'web4',
        branch: 'dev'
    },
    ...
}
```

#### Подключение:

```js
plugins: {
    'html-reporter/hermione': {
        enabled: true,
        pluginsEnabled: true,
        plugins: [{
            name: '@yandex-int/html-reporter-testcop-plugin',
            component: 'SuccessRate',
            point: 'result',
            position: 'before',
            config: {
                project: 'web4',
                tool: 'hermione'
            }
        }],
        ...
    },
    ...
}
```
