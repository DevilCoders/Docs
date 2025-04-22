## Файловая структура
```
.
└── src/
    ├── components/
    │   ├── Component/
    │   │   ├── Component.tsx
    │   │   ├── Component.test.tsx
    │   │   ├── Component.stories.tsx
    │   │   ├── Component.module.css
    │   │   ├── Component.types.ts // пропсы компонента
    │   │   ├── Component.config.ts // константы и объекты конфигураций
    │   │   ├── Component.utils.ts // вспомогательные функции
    │   │   └── index.ts
    │   ├── ComponentWithElements/
    │   │   ├── Element1/
    │   │   │   ├── Element1.tsx
    │   │   │   ├── Element1.test.tsx
    │   │   │   ├── Element1.stories.tsx
    │   │   │   ├── Element1.module.css
    │   │   │   ├── Element1.types.ts
    │   │   │   ├── Element1.config.ts
    │   │   │   └── Element1.tsx
    │   │   ├── Element2/
    │   │   │   ├── Element2.tsx
    │   │   │   ├── Element2.test.tsx
    │   │   │   ├── Element2.stories.tsx
    │   │   │   ├── Element2.module.css
    │   │   │   ├── Element2.types.ts
    │   │   │   ├── Element2.config.ts
    │   │   │   └── Element2.tsx
    │   │   ├── ComponentWithElements.test.tsx
    │   │   ├── ComponentWithElements.stories.tsx
    │   │   ├── ComponentWithElements.module.css
    │   │   ├── ComponentWithElements.types.ts
    │   │   ├── ComponentWithElements.config.ts
    │   │   └── index.ts
    │   ├── UserStatusProvider/
    │   │   ├── UserStatusProvider.tsx
    │   │   └── index.ts
    │   ├── Page/
    │   │   └── Page.tsx
    │   ├── withHoc/
    │   │   ├── withHoc.tsx
    │   │   ├── withHoc.types.ts
    │   │   └── index.ts
    │   └── useHook/
    │       ├── useHook.ts
    │       ├── useHook.types.ts
    │       └── index.ts
    ├── services/
    │   └── UserStatus/
    │       ├── UserStatus.ts
    │       ├── UserStatus.types.ts
    │       └── index.ts
    ├── types/
    │   ├── UserStatus.ts
    │   └── UserStatusType.ts
    ├── utils/
    │   ├── helperFunction.ts
    │   └── HelperClass.ts
    └── index.ts
```

## Названия в классах css
```
/* ComponentWithElements/ComponentWithElements.module.css */

.ComponentWithElements {}

.ComponentWithElements_modifierNameInCamelCase {}

.ComponentWithElements_modifierNameInCamelCase_modifierValueInCamelCase {}

.ComponentWithElements__inlineElement_mod_val {} /* элемент, для которого мы не выделяем отдельную папку */
```
