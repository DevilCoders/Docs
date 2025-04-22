## Глоссарий

📖 Хук - [React hook](https://ru.reactjs.org/docs/hooks-intro.html)
📖 hoc - Паттерн [High Order Component](https://reactjs.org/docs/higher-order-components.html)

## Именование

### Компоненты

-   ☝️ Из файлов компонента/модификатора/элемента экспортируются _только_ компонент/модификатор/элемент и тип/интерфейс пропсов
-   ☝️ Внутри папки компонента импорты относительные
-   ☝️ Импорты не из папки компонента – абсолютные
-   ☝️ Элементы, хуки и утилиты компонента _нельзя_ использовать вне компонента

📁 — папка, 📄 — файл, 📤 — экспортируемые сущности

```
📁 component-name
 │
 ├──📁 _mod-name
 │   ├──📄 component-name_mod-name.tsx — простой модификатор
 │   │   ├── 📤 hoc      withModName
 │   │   └── 📤 type     ComponentNameModNameProps
 │   │
 │   ├──📄 component-name_mod-name.css — стили
 │   │
 │   ├──📄 component-name_mod-name_mod-val.tsx — модификатор со значением
 │   │   ├── 📤 hoc      withModNameModVal
 │   │   └── 📤 type     ComponentNameModNameModValProps
 │   │
 │   └──📄 component-name_mod-name_mod-val.css —** **стили
 │
 ├──📁 __element-name
 │   ├──📄 component-name__element-name.tsx — элемент блока ComponentName
 │   │    ├── 📤 class   ComponentNameElementName
 │   │    └── 📤 type    ComponentNameElementNameProps
 │   │
 │   ├──📄 element-name.css — стили
 │   │
 │   └──📁 _mod-name
 │       ├──📄 component-name__elem-name_mod-name.tsx — простой модификатор
 │       │   ├── 📤 hoc  withModName
 │       │   └── 📤 type ComponentNameElemNameModNameProps
 │       │
 │       ├──📄 component-name__elem-name_mod-name.css — стили
 │       │
 │       ├──📄 component__elem-name-name_mod-name_mod-val.tsx — модификатор со значением
 │       │   ├── 📤 hoc  withModNameModVal
 │       │   └── 📤 type ComponentNameElemNameModNameModValProps
 │       │
 │       └──📄 component-name__elem-name_mod-name_mod-val.css — стили
 │
 ├──📁 component-name.assets — иконки, картинки
 │
 ├──📁 component-name.i18n — ключи переводов текстов
 │   └──📄 index.ts - экспорт
 │   └──📄 ru.ts - переводы конкретного языка
 │   └──📄 [<lang>.ts]...
 │
 ├──📁 component-name.utils(.ts) — вспомогательные функции
 │   └──📄 function-name.ts — функция
 │      ├── 📤 function  functionName
 │      └── 📤 type      FunctionNameParams
 │
 ├──📁 component-name.hooks — внутренние хуки компонента
 │   └──📄 use-hook-name.ts — хук
 │      ├── 📤 function  useHookName
 │      └── 📤 type      HookNameParams
 │
 ├──📄 component-name.types.ts — типы компонента
 │
 ├──📄 component-name.const.ts — константы использующиеся в компоненте. выносим только константы,
 │   │                           которые используются в нескольких файлах
 │   ├── 📤 function     cnComponentName
 │   └── 📤 string       keyset
 │
 ├──📄 component-name.tsx — компонент
 │   ├── 📤 class        ComponentName
 │   └── 📤 type         ComponentNameProps
 |
 ├──📄 component-name.container.tsx — обёртка, подключающая компонент к стору
 │   ├── 📤 class        ComponentNameContainer
 │   └── 📤 type         ComponentNameContainerProps
 │
 ├──📄 component-name.css — стили
 │
 ├──📄 component-name.stories.tsx — примеры компонента для Storybook
 │
 ├──📄 component-name.test.tsx — тесты компонента
 │
 └──📄 component-name.theme-name.tokens.yml — дизайн токены компонента
```

### Работа с api и react-query

-   ☝️ entity-name — имя сущности данных, например, Posts или Schools
-   ☝️ все, что относится к сущности лежит в папке этой сущности
-   ☝️ все хуки react-query экспортируются из entity-name-queries.ts

```
📁 src
└──📁 api
    ├──📁 entity-name
    |   ├──📄 entity-name.queries.ts — запросы react-query
    |   |   ├── 📤 useEntityNameQuery
    |   |   ├── 📤 useEntityNameInfinitQuery
    |   |   └── 📤 useEntityNameQueryWithAnotherEntityName — например, useSchoolsQueryWithPosts
    |   |
    |   ├──📄 entity-name.requests.ts — запросы данных ky
    |   |   └── 📤 getEntityNameRequest
    |   |
    |   ├──📄 entity-name.args.ts
    |   |   └── 📤 getEntityNameArgs — функция получения данных для ssr
    |   |
    |   └──📄 entity-name.const.ts — константы использующиеся в нескольких дргих файлах сущности
    |
    └──📁 helpers
        └──📄 get-pagination-params.ts — функция определяет можно ли еще запросить данные и с какими параметрами
```
