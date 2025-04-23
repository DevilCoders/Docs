## MgMenu

Меню. Предполагается к использованию в различных попапах или модальных окнах.

<img width="175" alt="menu" src="https://media.github.yandex-team.ru/user/1369/files/989f1980-da3b-11e9-8049-bb81e31277b7">

Состоит из нескольких компонентов: `MgMenu`, `MgMenuItem`, `MgMenuSeparator`. Пример использования:

```js
import { MgMenu, MgMenuItem, MgMenuSeparator } from '@yandex-turbo/components/MgMenu';

<MgMenu>
    <MgMenuItem>Без иконки</MgMenuItemSimple>
    <MgMenuItem isLoading iconTypeLeft={MgIconType.Share24}>Загружается</MgMenuItem>
    <MgMenuSeparator />
    <MgMenuItem iconTypeLeft={MgIconType.Ban24}>Заблокировать автора</MgMenuItem>
    <MgMenuItem
        iconTypeLeft={MgIconType.NotificationsOn24}
        caption="Вы будете получать уведомления о новых комментариях"
    >
        Получать уведомления
    </MgMenuItem>
    <MgMenuItem danger iconTypeLeft={MgIconType.Trash24}>Удалить пост</MgMenuItem>
</MgMenu>
```

В адаптере компонента, использующего меню необходимо вызвать `pushMgMenuSvgIconsToSprite` из `MgIcon`, чтоб иконки меню
попали в спрайт:
```js
import { pushMgMenuSvgIconsToSprite } from '@yandex-turbo/components/MgIcon/MgIcon.server';
...
public transform () {
    pushMgMenuSvgIconsToSprite(this.context);
}
```

### Модификаторы

| Свойство | Тип | Описание |
| ------- | ------- | ---------------------------------------- |
| `className?` | `String` | Микс. |

Свойства спредятся на внутренний MgListItem, поэтому см. перечень возможных свойств в нем.

### MgMenuItem
Элемент списка.

#### Модификаторы
| Свойство | Тип | Описание |
| ------- | ------- | ----------- |---------------------------------------- |
| `className?` | `String` | Микс. |
| `caption?` | `String` | | Серая подпись с пояснением действия. |
| `danger?` | `Boolean` | Делает текст красным. Нужен для потенциально опасных действий (требуется подключить `MgMenu/Item/_Danger/`).|
| `iconTypeLeft?` | `MgIconType` | Тип иконки, который нужно отобразить слева (требуется подключить `MgMenu/Item/_Danger/`).|
| `isLoading?` | `Boolean` | Отображение спиннера. |

#### Использование в turbojson
Адаптер MgMenuItem возвращает бандл с полным набором хоков. Таким образом в turbojson можно описать весь набор пропсов в
поле `props`, но в случае такого использования в ваш бандл попадет весь css кнопки, поэтому такой сценарий работы НЕ
РЕКОМЕНДУЕТСЯ. Пример:
```json
{
    "block": "mg-menu-item",
    "props": {
        "iconTypeLeft": "NOTIFICATIONS_ON_24",
        "caption": "Вы будете получать уведомления о новых комментариях"
    },
    "content": "Получать уведомления"
}
```

### MgMenuSeparator
Линия-разделитель.

#### Properties
| Свойство | Тип | Описание |
| ------- | ------- | ---------------------------------------- |
| `className?` | `String` | Микс. |
