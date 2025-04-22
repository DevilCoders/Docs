# Hot Keys

## HotKeyManager

[HotKeyManager.ts](packages/hotkeys/HotKeyManager.ts)

Модуль для централизованной подписки на *глобальные* горячие клавиши. Позволяет подписаться на keydown/keyup по названию клавиши и модификаторам.

## HotKey

[HotKey.tsx](packages/hotkeys/HotKey.tsx)

Компонент для подписки на глобальную комбинацию клавиш. При размонтировании автоматически отзывает подписку. Пример использования:

```jsx
// Вызывет handleEnterPress при срабатывании keyup на document с кодом клавиши Enter (клавиши-модификаторы не должны быть нажаты)
<HotKey keyCode="Enter" listener={handleEnterPress} />

// Ctrl+Escape, автоматически вызвать ev.preventDefault()
<HotKey ctrl keyCode="Escape" listener={handleCtrlEscapePress} preventDefault />

// Не вызывать листенер при повторных keydown, https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent#Auto-repeat_handling
<HotKey keyCode="Enter" eventName="keydown" noRepeats listener={handleEnterPress} />

// подписка на capture фазу
<HotKey keyCode="Enter" capture listener={handleEnterPress} />
```

## NamedHotKey

[NamedHotKey.ts](packages/hotkeys/NamedHotKey.ts)

Компонент для подписки на именованную комбинацию клавиш. Компонент создаётся с помощью функции `createNamedHotKey(hotKeys)`.

Пример создания:

```ts
import { createDescriptor } from '@mssngr/hotkeys/utils';
import { createNamedHotKey, HotKeyName } from '@mssngr/hotkeys';

const HotKeys = {
    MyCombo: {
        text: 'My combo description',
        descriptor: createDescriptor({
            all: { key: 'Enter', ctrl: true }, // Ctrl+Enter для всех
            mac: { key: 'Enter', meta: true }, // Cmd+Enter для маков
        }),
    },
    // ...
};

export const NamedHotKey = createNamedHotKey(HotKeys);
export type HotKey = HotKeyName<typeof HotKeys>;

```

Пример использования:

```jsx
<NamedHotKey name="MyCombo" listener={handleMyComboPressed} preventDefault />
<NamedHotKey
    name="MyCombo"
    eventName="keydown"
    capture
    noRepeats
    listener={handleMyComboPressed}
/>
```

## Как это работает

Каждая комбинация клавиш создаёт свой *стек слушателей*. При использовании `HotKeyManager` напрямую или компонентов для подписки на данную комбинацию, переданный  слушатель добавляется в соответствующий стек. При срабатывании события слушатели вызываются последовательно, в порядке, обратном их добавлению. В случае, если текущий слушатель а) вызывает `event.preventDefault()` или б) возвращает `true`, все последующие слушатели не будут выполнены.

При использовании `NamedHotKey` слушатели будут добавляться в тот же стек, что и при использовании `HotKey`/`HotKeyManager::subscribe` с дескриптором комбинации клавиш, соответствующим переданному имени комбинации.

## Примеры использования

Пусть есть модалка и попап, которые могут быть открыты независимо друг от друга. Добавление в каждый из них компонента HotKey таким образом, чтобы он рендерился только при открытом попапе и открытой модалке, позволяет реализовать их закрытие в порядке, обратном тому, в котором они были открыты. Например, если сначала был рендер с isModalVisible=true, а затем isPopupVisible=true, то нажатие Esc скроет сначала попап, а потом - модалку (и наоборот):

```jsx
{isModalVisible? (
    <div class="example-modal">
        <HotKey keyCode="Escape" listener={handleModalClose} preventDefault />
        ...modal content...
    </div>
) : null}

{isPopupVisible? (
    <div class="example-popup">
        <HotKey keyCode="Escape" listener={handlePopupClose} preventDefault />
        ...popup content...
    </div>
) : null}
```
