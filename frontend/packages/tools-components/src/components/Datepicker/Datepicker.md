# Datepicker

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/Datepicker'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

<!-- description:start -->
Компонент, предназначенный для выбора даты. Создан на основе [React Datepicker](https://reactdatepicker.com/), все пропсы прокидываются явно, частично поведение пропсов изменено, добавлена темификация, некоторые пропсы переименованы.
<!-- description:end -->

## Свойства

- `ariaLabelledBy?` `string` - [aria-labelledby](https://developer.mozilla.org/ru/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-labelledby_attribute)
- `autoComplete?` `string`
- `autoFocus?` `boolean`
- `className?` `string` 
- `controlRef?` `RefObject`
- `disabled?` `boolean`
- `id?` `string`
- `min?` `Date`
- `max?` `Date`
- `name?` `string`
- `onBlur?` `(React.FocusEvent):void`
- `onChange?` `(React.ChangeEvent):void`<br/>Обработчик изменения текста в поле.<br />Обратите внимание, что для получения значения используется onDateChange().<br/>Поведение onChange отличается между desktop, touch-pad и touch-phone.
- `onFocus?` `(React.FocusEvent):void`
- `onKeyDown?` `(React.KeyboardEvent):void`
- `placeholder?` `string`
- `readOnly?` `boolean`
- `required?` `boolean`
- `tabIndex?` `number`
- `title?` `string`
- `value?` `Date`
- `onDateChange?` `(Date | null): void` - Обработчик изменения даты
- `preventOpenOnFocus?` `boolean` - Запрет открытия дейтпикера при фокусировке на desktop
- `dateFormat?` `string`<br/>По умолчанию `'dd.MM.yyyy'`<br/>Формат отображения даты в поле на desktop и touch-pad
- `direction?` `Direction`<br/>По умолчанию `'bottom'`<br/>Допустимые значения: `'auto' | 'top' | 'right' | 'bottom' | 'left' | 'auto-start' | 'top-start' | 'right-start' | 'bottom-start' | 'left-start' | 'auto-end' | 'top-end' | 'right-end' | 'bottom-end' | 'left-end'`<br />Значение `'auto'` выбирает из `'top' | 'right' | 'bottom' | 'left'` на основе расстояния от инпута до края экрана. при выборе может ошибаться и отображать календарь за пределами экрана. Например, в углах
- `preventOverflow?` `boolean | Popper.PreventOverflow`<br/>По умолчанию `undefined`<br/>Позволяет передать параметры, управляющие корректировкой положения календаря для предотвращения выхода его за пределы окоймляющего элемента (viewport по умолчанию). За деталями [сюда](https://popper.js.org/docs/v2/modifiers/prevent-overflow/). Единственное изменение - если передано `true`, превращает в `{ enabled: true, boundariesElement: 'viewport' }`, `false` превращает в `undefined`
- `overflowPadding?` `Popper.PreventOverflow.padding`<br />Чтобы не приходилось разворачивать preventOverflow только для доопределения отступа дэйтапикера от края вьюпорта добавляет отступ для случая `preventOverflow === true`, для других случаев игнорируется
- `pverflowPreventionSelector?` `string`<br/>По умолчанию 
- `adjustDateOnChange?` `boolean`<br/>По умолчанию `true`<br/>Включает изменение даты при переключении месяца, года или управления с клавиатуры
<!-- props:end -->

## Модификаторы

<!-- modifiers:start -->
<!-- modifiers:end -->
