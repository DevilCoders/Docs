# EasterEgg

<!-- description:start -->
Используется для пасхалок. https://st.yandex-team.ru/SERP-114756
<!-- description:end -->

```js
import { EasterEgg } from '@yandex-draft-components/EasterEgg/touch-phone';
```

## Базовый вариант
```js
const App = () => {
  const [visible, setVisible] = React.useState(false);
  const openDrawer = React.useCallback(() => setVisible(true), [setVisible]);
  const closeDrawer = React.useCallback(() => setVisible(false), [setVisible]);

  return (
      <button onClick={openDrawer}>Открыть шторку</button>
      <EasterEgg
        visible={visible}
        onClose={closeDrawer}
        people={[
          {
            name: 'Имя Фамилия',
            position: 'Разработчик',
            avatar: 'https://avatars.mds.yandex.net/get-yapic/0/0-0/islands-retina-middle',
          },
          {
            name: 'Имя Фамилия',
            position: 'Тестировщик',
            avatar: 'https://avatars.mds.yandex.net/get-yapic/0/0-0/islands-retina-middle',
          },
        ]}
      />
  )
}
```


<!-- props:start -->
| Свойство        | Тип                                                                                                                                                                                                                                                               | По умолчанию    | Описание                                                                                                                                  |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| people          | `{ name: string, position: string, avatar: string }` []                                                                                                                                                                                                                                                         | —               | Список людей для показа в пасхалке                                                                              |
| onClose?        | `() => void`                                                                                                                                                                                                                                                      | —               | Функция, которая будет вызвана при попытке закрытия шторки.                                                                               |
| titleComponent? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | —               | Компонент шапки шторки.                                                                                                                   |
| keepMounted?    | `false \| true`                                                                                                                                                                                                                                                   | `true`          | Сохраняет контейнер в DOM после создания                                                                                                  |
| className?      | `string`                                                                                                                                                                                                                                                          | —               | Дополнительный класс                                                                                                                      |
| innerRef?       | `(instance: HTMLDivElement) => void \| RefObject<HTMLDivElement>`                                                                                                                                                                                                 | —               | Ссылка на корневой DOM-элемент компонента                                                                                                 |
| zIndex?         | `number`                                                                                                                                                                                                                                                          | —               | Задает слой `z-index`                                                                                                                     |
| visible?        | `false \| true`                                                                                                                                                                                                                                                   | —               | Делает попап видимым                                                                                                                      |
| scope?          | `RefObject<HTMLElement>`                                                                                                                                                                                                                                          | `document.body` | Ссылка на DOM-элемент, в котором размещается попап<br>Важно, чтобы контейнер имел `position: relative` для корректного позициоинирования. |
<!-- props:end -->
