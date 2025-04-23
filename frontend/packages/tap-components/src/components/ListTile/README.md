# ListTile

Компонент-примитив для удобного позиционирования контента, обрамленный иконками или другими блоками, например, `Checkbox`.

## Пример использования

```typescript jsx
import React from 'react'
import { ListTile } from '@yandex-int/tap-components/ListTile'

const App: React.FC = () => (
  <ListTile
      alignItems="center"
      trailing={
          <Text typography="control-s" color="secondary">
              Текст
          </Text>
      }
  >
      <Text typography="control-xl" color="primary">
          Текст
      </Text>
  </ListTile>
)
```

## Пример

{{%story:::tap-components-components-listtile--playground%}}

## Свойства

| Свойство    | Тип       | Описание                                  |
| ----------- | --------- | ----------------------------------------- |
| alignItems? | `"start" \| "end" \| "center" \| "baseline" \| "stretch"` | Выравнивание элементов вдоль основной оси |
| children    | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Основной контент компонента |
| className?  | `string` | Дополнительный класс у корневого DOM-элемента |
| inline?     | `false \| true` | Определяет ширину по содержимому |
| leading?    | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Содержимое перед `children` |
| leftSpace? | `"3xs" \| "2xs" \| "xs" \| "s" \| "m" \| "l" \| "xl" \| "2xl" \| "3xl" \| "4xl" \| "5xl" \| "6xl"` | Отступ слева от основного контента |
| onClick? | `(event: MouseEventHandler<HTMLDivElement>) => void` | Обработчик нажатия по ListTile |
| rightSpace? | `"3xs" \| "2xs" \| "xs" \| "s" \| "m" \| "l" \| "xl" \| "2xl" \| "3xl" \| "4xl" \| "5xl" \| "6xl"` | Отступ справа от основного контента |
| trailing?   | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | Содержимое после `children` |
