# Какие технологии и библиотеки мы используем в тестах

## Karma (http://karma-runner.github.io/)

Инструмент для запуска тестов

Настройки лежат в `{PROJECT}/karma.config.js`

Основные настройки:
```Javascript
...
  frameworks: ['mocha', 'expect', 'sinon'],
  files: [
      ...
      // helpers
      'test/helpers/unit_helpers.js',

      // Файлы с исходным кодом
      'hubs/jane/common.ru.js',
      'hubs/jane/jane.ru.js',

      'test/src/schema/schema.js',
      'test/mock/mock.js',

      // Файлы необходимые для тестов
      'test/src/jsx.globals.js',
      ...
      'test/src/filters.message-body.jsx.js',

      // Файлы с тестами
      'test/unit/*.js'
  ],
  port: 9876,
  browsers: ['PhantomJS'],
...
```

## Файловая структура тестов

Файловая структура тестов является зеркальным отражением
файловой структуры проекта.
Если файл лежит в папке `PROJECT/actoins/bar/bar.js` то тест для этого файла должен находится тут `PROJECT/test/unit/actions/bar/bar.js`.
Для файлов с расширением **.jsx**, тесты так же должны иметь расширение **.jsx**.
