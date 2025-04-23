# MessageBox

Визуальный компонент для уведомлений, плашек и других паттернов.

## Пример использования

```typescript jsx
import React from 'react';
import { compose, composeU } from '@bem-react/core';

import { MessageBoxPopup, Wrapper, withSizeM, withSizeS, withViewDefault, withViewPromo } from '@yandex-int/tap-components/MessageBox';

const MessageBox = compose(
    composeU(withViewDefault, withViewPromo),
    composeU(withSizeS, withSizeM),
)(MessageBoxPopup);

const App: React.FC = () => (
    <MessageBox
        opaque
        visible
        hasTail
        tailType="rounded"
        scope={scopeRef}
        direction="right-center"
        anchor={anchorRef1}
        view="default"
        size="s"
        layout="tooltip"
    >
        <Wrapper align="left">Подсказка</Wrapper>
    </MessageBox>
)
```

## Пример

{{%story:::tap-components-components-messagebox--playground%}}

## Свойства

| Свойство    | Тип         | По умолчанию | Описание   |
| ----------- | ----------- | ------------ | ---------- |
| actions? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — | Кнопка или набор кнопок, которые будут размещены внизу компонента |
| anchor? | `RefObject<HTMLElement>` | — | Элемент, относительно которого позиционируется попап |
| background? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — | Элемент, который будет размещен на фоне компонента |
| className? | `string`   | — | Дополнительный класс у корневого DOM-элемента |
| corner? | `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — | Элемент, который будет размещен в углу компонента |
| direction? | `Direction | Direction[]` | — | Направление для раскрытия компонента |
| hasTail? | `false \| true` | — | Включает/отключает хвостик у компонента |
| innerRef? | `RefObject<HTMLDivElement>` | — | Ссылка на корневой DOM-элемент компонента |
| layout? | `"tooltip" \| "plain" \| "functional"` | `'plain'` | Раскладка компонента |
| onClick? | `(event: MouseEventHandler<HTMLDivElement>) => void` | — | Обработчик, вызываемый при срабатывании события click |
| onClose? | `() => void` | — | Обработчик клика на close-элемент и индикатор того, что close надо показать |
| opaque? | `false \| true` | — | Делает фон непрозрачным |
| scope? | `RefObject<HTMLElement>` | `document.body` | Ссылка на DOM-элемент, в котором размещается попап.<br>Важно, чтобы контейнер имел `position: relative` для корректного позиционирования. |
| tailRef? | `(instance: HTMLDivElement) => void \| RefObject<HTMLDivElement>` | — | Ссылка на DOM-элемент хвостика |
| tailType? | `"default" \| "rounded"` | `'default'` | Тип хвостика | visible? | `false \| true` | — | Делает попап видимым |
