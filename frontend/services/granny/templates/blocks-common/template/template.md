# Шаблоны
## Особенности
Шаблоны – это особые блоки, API которых доступно из адаптера.  Напрямую шаблоны не вызываются. Аргументы прокидываются и генерируются автоматически, из данных, возвращенных адаптером.

Код шаблонов лежит в отдельной папке `templates`, на том же уровне в файловой системе, что и `construct`, и `adapters`.  
Имя шаблона в коде должно начинаться с префикса `template-`, например, `template-bno`.

От обычных блоков они отличаются двумя свойствами.
### 1. Только шаблоны могут вызываться из адаптера
Шаблоны – это сущности, c API которых взаимодействуют адаптеры.

**Пример:**
```js
/* Данные из бэкэнда */
doc: {
  construct: {
     type: 'my-adapter',
     field1: 'O_O'
  }
}
```
```js
/* Результат, возвращаемый адаптером my-adapter */
return {
  template: 'card', // Если поле template в адаптере не указано, то считается, что используется шаблон 'default'
  arg1: field1 // Поле arg1, которое передается в API шаблона 'card'
  /* ... */
}
```

### 2. Шаблоны могут собираться из нескольких адаптеров
Шаблоны могут строиться несколькими адаптерами одновременно. Это распространяется только на top-level элементы Шаблона

Если для снипета пришло несколько адаптеров, они могут построить шаблон совместно. Сами адаптеры друг о друге при этом ничего не знают. Если адаптеры пытаются заполнить одинаковые поля, то приоритет у того адаптера который пришел в данных первым.

**Пример:**
```js
/* Данные из бэкэнда */
doc: {
  construct: [
    {
      type: 'my-adapter',
      field1: 'O_O',
      complexField: {
        field1: '(^_^)~~'
      }
    },
    {
      type: 'her-adapter',
      field1: 'X_X',
      field2: 'T_T',
      complexField: {
        field1: '(O_O)',
        field2: '--------'
      }
    }
  ]
}
```
```js
/* Результат, возвращаемый адаптером my-adapter */
return {
  template: 'default', // Если поле template в адаптере не указано, то считается что используется шаблон 'default'
  arg1: field1 // Поле arg1, которое передается в API шаблона 'card'
  /* ... */
}

/* Результат, возвращаемый адаптером her-adapter */
return {
  template: 'default', // Если поле template в адаптере не указано, то считается что используется шаблон 'default'
  arg1: field1, // Поле arg1, которое передается в API шаблона 'card'
  arg2: field2
  /* ... */
}
```

В результате будет вызван адаптер default, и он будет использовать следующие значения полей
```js
arg1 === 'O_O',
arg2 === 'T_T',
complexField === {
  field1: '(^_^)~~'
}
```
Обратите внимание что `ComplexField` не смержилось.

## Внутреннее устройство.
Сигнатура и аргументы у шаблона выглядят следующим образом. Так, например, мог бы выглядеть шаблон для примеров из предыдущего раздела.

```js
/**
 * Мой супер крутой шаблон.
 *
 * @params {TemplateDefaultPair} datasets.
 *
 * @returns {Bemjson}
 */
blocks['template-default'] = function(datasets) {
  var createElem = _.partial(blocks['template__elem'], 'default', datasets);
  return {
    block: 'template',
    mods: { type: 'default' },
    content: [
        createElem('arg1'),
        createElem('arg2'),
        createElem('complexField')
    ]
  }
}


/**
 * @typedef {object} TemplateDefaultPair
 *
 * @property {Context} context
 * @property {TemplateDefault} data
 */

/**
 * @typedef {Object} TempalteDefault
 *
 * @property {BlahBlah} [arg1] - апи блока blah-bla. 
 * @property {BlahBlah} [arg2] - апи блока blah-bla.
 * @property {ComplexBlahBlah} ComplexField - апи блока Complex.-blah-blah
 */
 ```

Тут стоит обратить внимание на хелпер `blocks['template__elem']`, который используется через partial. Этот хелпер выбирает поле с соответствующим именем из набора `datasets` и рисует его с помощью одноименного элемента.
Для того чтобы хэлпер корректно работал, в файл с шаблоном нужно добавить следующий код:
```js
/**
 * @params {Context} context
 * @params {BlahBlah} dataset
 *
 * @returns {Bemjson}
 */
blocks['template-default__arg1'] = function(context, dataset) {
  return blocks['blah-blah'](context, dataset) //предположим, что такой блок есть
}

/**
 * @params {Context} context
 * @params {BlahBlah} dataset
 *
 * @returns {Bemjson}
 */
blocks['template-default__arg2'] = function(context, dataset) {
  return blocks['blah-blah'](context, dataset) //предположим, что такой блок есть
}

/**
 * @params {Context} context
 * @params {ComplexBlahBlah} dataset
 *
 * @returns {Bemjson}
 */
blocks['template-default__complexField'] = function(context, dataset) {
  return blocks['complex-blah-blah'](context, dataset) //предположим, что такой блок есть
}
```

**Важно: У шаблона может быть собственная статика. Если это так, то его так же, как и блок, нужно выносить в отдельный бандл.**

## Шаблон [Composite](http://docs.serp.yandex.ru/types/TemplateComposite)
### Использование
Composite предназначен для отрисовки стека шаблонов и блоков в рамках одного документа в результатах поиска.
Шаблон обрабатывает все сниппеты в рамках документа и отрисовывает их как один поисковый результат. Это проиллюстрировано на следующем примере.

[**Пример:**](https://forever.si.yandex-team.ru/?hash=1223678393)
```js
"construct": [
  {
    "type": "my-adapter-type",
    "template": "composite",
    "items": [
      {
        "block": "paragraph",
        "text": "Проверяем, что айтемы из двух адаптеров будут мержиться."
      },
      {
        "block": "paragraph",
        "text": "Этот параграф вместе с предыдущим приходят из первого адаптера."
      }
    ]
  },
  {
    "type": "my-second-adapter-type",
    "template": "composite",
    "items": [
      {
        "block": "paragraph",
        "text": "А этот – из второго."
      }
    ]
  }
]
```
Такая конструкция отрисует все параграфы друг под другом, сложив их в элементы одного шаблона Composite.
То же самое можно проделать с любыми блоками или шаблонами (см. [пример](https://forever.si.yandex-team.ru/?hash=2846186226)).

С помощью Composite можно собирать практически что угодно. Например, пользуясь свойством `gap`, можно имитировать несколько ответов подряд (`gap: 'm'`), складывать разные блоки в рамках одного ответа (`gap: 's'`), создавать "склеенные" карточки (`gap: 'none'`).

Подробнее про остальные возможности Composite читайте в [документации к нему](http://docs.serp.yandex.ru/types/TemplateComposite).

**Важно:** при сборке фичи старайтесь использовать готовые конструкции (`organic`, `fact`, `object-badge` и т.д.).

### Вложенность
С помощью Composite можно собирать сложносочиненные сниппеты и колдунщики, вкладывая блоки или другие шаблоны друг в друга.

[**Пример:**](https://forever.si.yandex-team.ru/?hash=1766388973)
```js
"construct": {
  "template": "composite",
  "fold": { "height": 200 },
  "gap": "m",
  "items": [
    {
      "template": "object-badge",
      "object-badge": { ... },
      "items": [ ... ]
    },
    { "block": "button", "text": "test" },
    {
      "template": "composite",
      "gap": "none",
      "items": [
        {
          "template": "fact",
          "fact": { ... }
        },
        {
          "block": "button",
          "text": "Больше информации",
          "url": "..."
        }
      ]
    }
  ]
}
```
Этот пример выведет Composite, часть которого скрыта с помощью [fold](http://docs.serp.yandex.ru/blocks/fold), содержащий внутри набор блоков и еще один Composite с [фактовой карточкой](http://docs.serp.yandex.ru/blocks/fact).

### Развитие
Стоит помнить, что шаблон Composite – это work in progress. По мере выполнеия задачи [SERP-41190](https://st.yandex-team.ru/SERP-41190) шаблон Composite планируется развить в более универсальную сущность, которая, скорее всего, будет представлять из себя просто часть core конструктора. За основу принимается Карточка – 
https://depot.serp.yandex.ru/wiki/libs/serp/card/.
Шаблоны перестанут существовать как отдельный уровень абстракции, и возникающий у многих вопрос "Что мне писать – блок или шаблон?" перестанет быть актуальным.
