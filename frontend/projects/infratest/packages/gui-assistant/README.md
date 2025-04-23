# gui-assistant

Плагин для [hermione](https://github.com/gemini-testing/hermione).
Добавляет возможность реиспользования результатов прогонов тестов в Sandbox или результатов, опубликованных в произвольном static-хранилище

## Установка

```bash
npm install @yandex-int/gui-assistant --save-dev --registry https://npm.yandex-team.ru
```

## Подключение
```js
plugins: {
    '@yandex-int/gui-assistant/gemini': { // @yandex-int/gui-assistant/hermione
        enabled: true, // by default
        reportPath: 'gemini-report', // путь для сохранения скачанного репорта
        hostnameReplacer: /.+\.yp-c\.yandex\.ru/, // по умолчанию подменяет gui hostname на hostname операционной системы при запуске на qyp машинке

        // опции для поиска PR, созданного из текущей локальной ветки
        owner: 'serp',
        repo: 'granny',
        forks: ['search-interfaces']
    }
}
```

## Использование
```bash
./node_modules/.bin/gemini gui --help
```
