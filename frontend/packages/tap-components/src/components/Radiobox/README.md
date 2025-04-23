# Radiobox

Компонент для создания радиопереключателя.

## Пример использования

```typescript jsx
import React, { useState } from 'react'
import { compose } from '@bem-react/core'
import {
    Radiobox as RadioboxBase,
    withSizeM,
    withViewDefault,
} from '@yandex-int/tap-components/Radiobox'

const Radiobox = compose(
    withSizeM,
    withViewDefault,
)(RadioboxBase)

const App: React.FC = () => {
    const [value, setValue] = useState('value1')

    return (
        <Radiobox
            size="m"
            view="default"
            value={value}
            options={[
                { label: 'Радио 1', value: 'value1' },
                { label: 'Радио 2', value: 'value2' },
                { label: 'Радио 3', value: 'value3' },
            ]}
            onChange={(event) => setValue(event.target.value)}
        />
    )
}
```

## Пример

{{%story:::tap-components-components-radiobox--playground%}}

## Свойства

| Свойство	 	| Тип 																																																																| По умолчанию 		| Описание 																							|
| -------------	| -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	| ----------------- | ------------------------------------------------------------------------------------------------- |
| children? 	| `string \| number \| false \| true \| {} \| ReactElement<any, string \| ((props: any) => ReactElement<any, string \| ... \| (new (props: any) => Component<any, any, any>)>) \| (new (props: any) => Component<any, any, any>)> \| ReactNodeArray \| ReactPortal` | — 				| Набор переключателей c использованием `Radio` элемента<br>Может быть использовано вместо `options`|
| className? 	| `string` 																																																															| — 				| Дополнительный класс у корневого DOM-элемента 													|
| disabled? 	| `false \| true` 																																																													| — 				| Неактивное состояние всей группы переключетелей 													|
| innerRef? 	| `(instance: HTMLSpanElement) => void \| RefObject<HTMLSpanElement>` 																																																| — 				| Ссылка на корневой DOM-элемент компонента 														|
| name? 		| `string` 																																																															| — 				| Имя для всех `Radio` элементов 																	|
| onChange? 	| `(event: ChangeEvent<HTMLInputElement>) => void` 																																																					| — 				| Обработчик изменения значения 																	|
| options? 		| `RadioOptionProps[]` 																																																												| `[]` 				| Набор переключателей<br>Может быть использовано вместо `children` 								|
| value? 		| `string` 																																																															| — 				| Текущее выбранное значениее в группе 																|
