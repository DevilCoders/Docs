Компонент Button
---

Stories: https://yandexclassifieds.github.io/realty-frontend/vertis-react/?selectedKind=Components%7CButton&selectedStory=button

Выглядит так:

![example.png](./example.png)

Или так: (если выбрана тема realty)

![example-realty.png](./example-realty.png)

Темы
---

Поддерживаются 2 темы (`theme`)
- islands
- realty (https://www.figma.com/file/dna5pKOYpAEzYyApTHUzLXJ3/Realty-guide?node-id=0%3A1)

Для `islands` досутпны следующие `view`:

`'action', 'pseudo', 'plain', 'green', 'blue', 'grey'`

Для `realty`:

`'yellow', 'green', 'blue', 'light-blue', 'soft-blue', 'red', 'grey', 'transparent-black', 'transparent-white'`

Обертки
---
Существует VasButton (realty-core/view/react/deskpad/components/VasButton), который представляет из себя обычную кнопку с темой `realty`, но маппит названия услуг (prop `service`) в цвета кнопок согласно нашим гайдам:
```js
const SERVICE_VIEW_MAP = {
    premium: 'action',
    promotion: 'blue-soft',
    raising: 'green'
};
```

Кастомная прозрачность
---
Использование псевдоэлемента в качестве background позволяет
управлять прозрачностью текста и фона поотдельности.

Выглядеть это может примерно так:
```css
.Button-stories__transparent-bg:before {
    opacity: 0.3;
}

.Button-stories__transparent-text > .Button__text {
    opacity: 0.3;
}
```

посмотреть можно тут:
https://yandexclassifieds.github.io/realty-frontend/vertis-react/?selectedKind=Components%7CButton&selectedStory=custom%20opacity
