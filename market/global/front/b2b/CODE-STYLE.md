# MST

1. #### Не используйте types.reference
2. #### Если нужна ссылка, реализуйте ее через resolveIdentifier
3. #### Если все еще хотите использовать types.reference, то обращение к ней только через [tryReference](https://mobx-state-tree.js.org/API/index#tryreference).

# Imports & Exports

1. #### Запрещен импорт внутренних сущностей из другого модуля. Импорт разрешен только из корня другого модуля.
   - <span style="color:red">Плохо: `import Model from 'module/models/Model'`</span>
   - <span style="color:green">Хорошо: `import Model from 'module'`</span>
   - Мотивация: Для соблюдения [инкапсуляции](<https://ru.wikipedia.org/wiki/Инкапсуляция_(программирование)>)
2. #### Нельзя использовать wildcard export.
   - <span style="color:red">Плохо: `export * from './hooks'`</span>
   - <span style="color:green">Хорошо: `export {useMetrika, useStore, useEnv} from './hooks'`</span>
   - Мотивация: Для соблюдения [инкапсуляции](<https://ru.wikipedia.org/wiki/Инкапсуляция_(программирование)>). Чтобы случайно не пролить лишний export.

# React компоненты

## Структура директории React-компонента

Типичная структура выглядит так:

```
.
└── ComponentName/

    ├── ComponentName.tsx

    ├── ComponentName.style.ts

    ├── ComponentName.stories.tsx

    ├── ComponentName.test.tsx -

    └── index.ts
```

- #### `ComponentName.tsx` - Код компонента

  ```
  export interface ComponentNameProps {
    // ...
  }

  const useStyles = makeStyles(ComponentNameStyles)

  const ComponentName: React.FC<ComponentNameProps> = (props) => {
    const c = useStyles()
    // ...
  }
  ```

- #### `ComponentName.style.ts` - JSS Стили компонента

  ```
  import {createStyles} from '@material-ui/core/styles'

  const ComponentNameStyles = createStyles({
    className: {}
  })

  export default ComponentNameStyles
  ```

- #### `ComponentName.stories.tsx` - Сторибук компонента

  ```
  import React from 'react'
  import {Story, Meta} from '@storybook/react'

  export default {
  title: 'ComponentName',
  component: ComponentName
  } as Meta

  const Template: Story<ComponentNameProps> = (args) => <ComponentName {...args} />

  export const Story1 = Template.bind({})
  Story1.args = {}
  ```

  - Должен отображать все возможные состояния компонента. (насколько это возможно)
  - Должны быть отсняты скриншоты со всех сторис с помощью Loki.

- #### `ComponentName.test.tsx` - Тесты на интерактивную часть компонента. Все, что нельзя покрыть скриншотами сторибук.
- #### `index.ts` - Реэкспорты. Представляет собой внешний интерфейс необходимый для работы с компонентом.
  `export { default } from './ComponentName'`
