## JavaScript {#javascript}

### Общая информация {#common}

В результате выполнения вкладки JavaScript должны быть экспортированы данные для отрисовки вики-текста.

### Доступные методы {#available-methods}

* **`ChartEditor.getParams()`** — возвращает объект с нормализованными параметрами.

* **`ChartEditor.getLoadedData()`** — возвращает объект с данными, запрошенными на вкладке Urls.

* **`ChartEditor.updateConfig(config)`** — доопределяет результат вкладки [Config](config.md) аргументом `config`.

### Пример {#example}

```js
// формируем вики-текст

const text1 = 'Полужирный текст';
const text2 = 'Моноширинный текст';
// используем шаблонную строку
const wiki1 =
`**${text1}**
//Курсивный текст//
__Подчеркнутый текст__
##${text2}##`;

const text3 = 'Вопрос';
const text4 = 'Замечание';
// используем конкатенацию строк с переходами на новую строку (\n)
const wiki2 = '\n--Зачеркнутый текст--'
    + '\n??' + text3 + '??\n'
    + '!!' + text4 + '!!\n'
    + '!!(син)Текст синего цвета!!';

// экспортируем данные для отрисовки
module.exports = {
    content: wiki1 + wiki2
};
```
