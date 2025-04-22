# Использование [PostCSS](https://github.com/postcss/postcss)

PostCSS позволяет использовать только определенную функциональность с помощью системы плагинов. Ниже описаны используемые в проекте плагины с примерами.

## Импорты стилей

[`@doctorwork/postcss-autoimport`](https://github.com/rajdee/postcss-autoimport) автоматически импортирует общие переменные и миксины.

[`postcss-import`](https://github.com/postcss/postcss-import) позволяет импортировать стили, используя `@import`.

```
@import './common/some-other-styles.css';
```

> Расширение импортируемого файла обязательно.

## [Переменные](https://github.com/jonathantneal/postcss-advanced-variables#variables)

```
$string: string-value;
$pixels: 10px;
$color: rgb(0, 0, 0);
$color-array: (red, blue, yellow);
$map: (
  a: 1,
  b: 2,
  c: 3
);
```

Для использования переменных в селекторах используйте `$(variable)`, например, `&.__$(item)`.

> Строчные переменные указываются без кавычек.

## [Миксины](https://github.com/jonathantneal/postcss-advanced-variables#mixin-include-and-content-rules)

```
// Создание миксина
@mixin name-of-your-mixin($first-arg, $second-arg: default-value) {
    // ...
}

// Использование
@include name-of-yor-mixin($color, not-default-value);
```

## [Циклы](https://github.com/jonathantneal/postcss-advanced-variables#for-and-each-rules)

Итерация по массивам с помощью `@each`.

> Массивы должны быть в скобках и обязательно разделены запятой с пробелом: `(value, another-value, one more)`.

```
@each $value $index in $color-array {
    &._index_$(index) {
        color: $value;
    }
}

// Так же можно итерироваться по хешам:
@each $number $letter in $map {}

@for $number from 2 to 6 {}
```

> Заметьте, что запятая **не ставится** между значением и ключом в `@each`.

## Вычисления

[`postcss-automath`](https://github.com/EverledgerIO/postcss-automath) позволяет делать вычисления в одинаковых единицах измерения.

## Вложенность

[`postcss-nested`](https://github.com/postcss/postcss-nested) позволяет использовать вложенность стилей.

```
.my-class {
    &__item {}

    // Использование с корневым селектором
    .root-class & {}
}
```

## Вставка SVG

[`postcss-inline-svg`](https://github.com/TrySound/postcss-inline-svg) позволяет инлайнить SVG изображения через декларацию `svg-load(url)`.

Для исключения пересечений в ID фильтров у SVG, при добавлении новой иконки в проект рекомендуется запустить на ней `make min-svg DIR="path/to/icon.svg"`.

Таким образом она минифицируется и заодно все ее ID получат уникальный префикс.
