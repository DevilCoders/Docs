## MgButtonIcon
Кнопка-иконка на основе кнопки lego. Обычно используется для нажимаемых иконок. Полезна тем, что расширяет зону клика по ним.

<img width="120" alt="MgButtonIcon" src="https://media.github.yandex-team.ru/user/1369/files/a2626680-fa56-11e9-914c-857225164e2b">

### Props

| Свойство | Тип | По умолчанию | Описание |
| ------- | ------- | ----------- | ---------------------------------------- |
| `type` | `MgIconType` |  | Тип иконки (MgIcon). Также необходимо в каком-либо адаптере пушнуть нужные иконки через `ctx.assets.pushSvgToSprite` |
| `size` | `MgButtonIconSize` |  | Размер кнопки-иконки. |
| `theme` | `MgButtonIconTheme` |  | Цветовая тема кнопки-иконки. Цвета аналогичны темам MgButton |
| `appearance?` | `MgButtonIconAppearance` | MgButtonIconAppearance.LIGHT | Внешность кнопки-иконки (темное/светлое оформление). |
| `pin?` | `MgButtonIconPin` | MgButtonIconPin.ROUND_ROUND | Закругленность кнопки-иконки (квадртная или круглая). |
| `disabled?` | `Boolean` |  | Делает кнопку задизейбленой. |
| `className?` | `String` |  | Микс. |

### Использование
Компонент можно использовать напрямую в turbojson, но в таком случае он принесет с собой весь набор иконок MgIcon.
При использовании компонента в tsx, необходимо самим в адаптере озаботиться о добавлении нужных svg-ассетов в спрайт,
например:
```js
ctx.assets.pushSvgToSprite({
    name: 'mg-icon__comment_24',
    icon: IconComment24,
});

ctx.assets.pushSvgToSprite({
    name: 'mg-icon__like_24',
    icon: IconLike24,
});
```
