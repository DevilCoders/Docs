# Темизитор внешней капчи

Виджет темизатор для внешней капчи.
Виджет представляет из себя SPA-приложение. Основной способ использования виджета - встраивание его в качестве iframe. Общение с iframe'ом происходит через post-message.

## 🔗 Содержимое

* [Подключение](#подключение)
* [API](#api)
* [Разработка](#разработка)

## Подключение

```html
<script>
  function handleThemerReady(event) {
    if (event.data === 'themer-ready') {
      // Знаем что themer работает, делаем что хотим...
      // Например отправляет изменение одного токена
      event.source.postMessage({
        type: 'single',
        payload: {
          name: 'variable-name',
          value: 'new-variable-value'
          }
        });

      // Удалить обработчик
      window.removeEventListener('message', handleThemerReady);
    }
  }

  window.addEventListener('message', handleThemerReady);
</script>

<iframe src="https://captcha-test.yandex-team.ru/themer.html"></iframe>
```

## API

Описание API для работы с виджетом.

### Метод установки значения токенов

Данные методы используются для передачи изменений пользователей.

```js
// Передача одного изменения.
iframe.postMessage({
  type: 'single',

  payload: {
    name: 'variable',
    value: 'value'
  }
});

// Передача нескольких изменений.
iframe.postMessage({
  type: 'multiple',

  payload: [
    {
      name: 'variable1',
      value: 'value1'
    },
    {
      name: 'variable2',
      value: 'value2'
    },
  ]
});

// Передача конфига в формате ключ-значение.
// Для ключей, которые не были указаны, используется значение по-умолчанию.
iframe.postMessage({
  type: 'json',

  payload: {
    'variable1': 'value1',
    'variable2': 'value2',
  }
});

```

### Метод установки статуса

Данный метод используется для изменения типа отображения капчи.
Доступные типы отображения: стандартный, успешное выполнение(с галочкой), загрузка(со спинером), ошибка.

```js
iframe.postMessage({
  type: 'status',

  // Список возможных значений: 'default', 'success', 'loading', 'error'
  payload: 'success',
});
```

### Метод установки сложности

Данный метод используется для изменения типа сложности картинки в капче. Параметер меняет отображаемую картинку.
Доступные типы сложности: простой, средний, сложный.

```js
iframe.postMessage({
  type: 'complexity',

  // Список возможных значений: 'easy', 'medium', 'hard'
  payload: 'hard',
});
```

## Разработка

### Запуск

1. Установить зависимости: `npm ci`.
2. Запустить дев-сервер: `npm run start`.

### Тестирование

Запуск unit-тестов: `npm t`.

Запуск hermione-тестов без gui: `npm run hermione:build && npm run hermione:test`.

Запуск hermione-тестов с gui: `npm run hermione:build && npm run hermione:gui`.


### Билд

Билд происходит командой: `npm run build`.

### Выкладка

Выкладка происходит вручную. Для этого нужно обратиться к @tyamgin.
