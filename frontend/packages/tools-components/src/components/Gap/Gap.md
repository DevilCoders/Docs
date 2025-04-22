# Gap

<a
  href='https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tools-components/src/components/Gap'
  target='_blank'>
  <img
    src='https://badger.yandex-team.ru/custom/[Исходники]/[Github][green]/badge.svg'
  />
</a>

Компонент содержит набор svg-иконок и css-переменных для всех типов отсутствий.

В `Gap.css` файле блока объявлена переменная `$staff-gap-types` со списком типов отсутствий

В `Gap.color.css` объявлены цвета для типов отсутствий

- `--staff-color-gap-{тип отсутствия}` обычный цвет отсутствия
- `--staff-color-gap-{тип отсутствия}-light` бледный цвет отсутствия

```css
@import './Gap.css';
@import './Gap.color.css';

@each $type in $staff-gap-types {
    .gap_type_$type {
        background-color: var(--staff-color-gap-$(type));
        background-image: url('./Gap/Gap.assets/$(type).svg');
    }
}
```
