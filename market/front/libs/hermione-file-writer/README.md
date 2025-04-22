Hermione File Writer
===========

## Description
Плагин для [Гермионы](https://github.com/gemini-testing/hermione/), позволяющий собирать необходимые данные и записывать их в файл.

Сбор данных осуществляется во внутренний объект плагина и выводится в выходной файл в виде отформатированного JSON-объекта.

## Configuration
Параметры конфигурации плагина указываются в [соответствующей секции](https://github.com/gemini-testing/hermione/#plugins) файла конфигураций Hermione-ы.

Параметры:
#### `{string} fileName` 
Имя файла, в который будет производиться запись.

## API
### Test context
Плагин расширяет контекст выполнения тестов, предоставляемый [Mocha](https://mochajs.org/):

___

#### `extendOutputObj(content)`
Добавляет содержимое в объект, который впоследствии будет записан в файл (output-object).

**Аргументы:**

- `{Object} content` - Объект, которым будет расширен (используется [lodash](https://lodash.com/docs/4.17.4#assignIn)) существующий output-object.
