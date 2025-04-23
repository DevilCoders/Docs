# template-error-collector

Плагин для [gemini](https://github.com/gemini-testing/gemini) и [hermione](https://github.com/gemini-testing/hermione) для отслеживания событий типа ERROR и WARNING в логах выполнения шаблонов.

## Установка

```bash
npm install @yandex-int/template-error-collector --save --registry https://npm.yandex-team.ru
```

## Подключение
```js
plugins: {
    '@yandex-int/template-error-collector/hermione': { // @yandex-int/template-error-collector/gemini
        enabled: true, // by default
        reportPath: 'template-errors.txt' // by default,
        failOnErrors: true // by default
    }
}

```

Если во время прогона тестов в шаблонах были сообщения типа error или warning, то они сохранятся в файл. Далее в зависимости от значения опции `failOnErrors` либо прогон тестов завершится с ошибкой, либо в консоль будет выведено предупреждение о наличии ошибок в шаблонах.
