## Описание

Блок `pointerfocus` это хелпер, помогающий применять стили к элементам,
получившим фокус с помощью указателя (мышь, палец) и клавиатуры.


## Принцип работы

При наступлении события `focusin` скрипт выставляет элементу `html` класс `pointerfocus` или `utilityfocus`. Наличие класса `pointerfocus` говорит о том, что перед этим произошли события `pointerdown`,
`pointerup` или `click`. Наличие класса `utilityfocus` говорит о том, что эти события накануне не произошли.

Таким образом, класс `pointerfocus` указывает на то, что фокус был получен мышью/пальцем,
а класс `utilityfocus` говорит о том, что фокус  
был получен другим способом, скорее всего с клавиатуры.


## Использование

```css
html.utilityfocus button:focus {
    outline: 2px solid orange;
}

html.pointerfocus button:focus {
    outline: 2px solid green;
}
```


## Примечания

1. Блок использует jQuery, pointer-события и работает в __IE8+__ и всех актуальных браузерах.

1. Блок не конфликтует с библиотекой [FastClick], если только вы не применяете ее непосредственно к `window`.

1. В Chrome 36, когда окно становится активным, браузер программно возвращает фокус
на `document.activeElement`. Например, если мышкой поставить фокус на инпуте, затем
переключиться на другую вкладку и вернуться обратно, то инпут вновь окажется в фокусе,
но вместо `pointerfocus` будет выставлен класс `utilityfocus`. Это ожидаемое поведение.


## Дополнительно

- http://www.sitepoint.com/when-do-elements-take-the-focus/


[fastclick]: https://github.com/ftlabs/fastclick
