# Наименование и расположение файлов

## React компоненты

Компонент и стили для компонента называем по имени папки.

Иллюстрации лежат в папке `images`.

Для добавление примера в `storybook` используем файл `<ComponentName>.stories.(tsx|mdx)`.

```
.
└── Button
    ├── Button.scss
    ├── Button.stories.tsx
    ├── Button.tsx
    ├── README.md
    └── images
        └── cat.png
```

Всегда экспортируем компонент дефолтным экспортом, кроме того обязательно экспортируем тип его пропсов:

```tsx
export interface IButtonProps {}

const Button: React.FC<IButtonProps> = () => {};

export default Button;
```

### Компоненты-приложения

Представляют из себя компоненты, в которых есть `Switch` и `Route` с компонентами-страницами.

Имеют суффикс `App`.

Общие приложения лежат в папке `/src/applications`.

```
.
└── src
    └── applications
        └── IndexApp
            └── IndexApp.tsx
```

Приложения вертикалей лежат в папках `/src/projects/<projectName>/applications`.

```
.
└── src
    └── projects
        └── hotels
            └── applications
                └── BookApp
                    └── BookApp.tsx
```

### Компоненты-страницы

Имеют суффикс `Page`.

Общие страницы лежат в папке `/src/pages`.

```
.
└── src
    └── pages
        └── IndexPage
            └── IndexPage.tsx
```

Страницы вертикалей лежат в папках `/src/projects/<projectName>/pages`.

```
.
└── src
    └── projects
        └── hotels
            └── pages
                └── SearchPage
                    └── SearchPage.tsx
```

### Компоненты

Общие компоненты лежат в папке `/src/components`

```
.
└── src
    └── components
        └── Button
            └── Button.tsx
```

Компоненты вертикалей, которые используются на нескольких страницах, лежат в папках `/src/projects/<projectName>/components`

```
.
└── src
    └── projects
        └── hotels
            └── components
                └── Address
                    └── Address.tsx
```

Достаточно специфичные компоненты, которые используются только внутри какого-то определенного компонента, лежат в папке `components` этого компонента и не должны иметь префикс этого компонента.

```
.
└── src
    └── projects
        └── hotels
            └── components
                └── Address
                    └── Address.tsx
                    └── components
                        └── Title
                            └── Title.tsx

```

```
.
└── src
    └── projects
        └── hotels
            └── pages
                └── SearchPage
                    └── SearchPage.tsx
                    └── components
                        └── HotelCard
                            └── HotelCard.tsx

```

```
.
└── src
    └── projects
        └── hotels
            └── pages
                └── SearchPage
                    └── SearchPage.tsx
                    └── components
                        └── HotelCard
                            └── HotelCard.tsx
                            └── components
                                └── Title
                                    └── Title.tsx

```

### Контейнеры

Лежат в папке с компонентом и имеют суффикс `Container`, чтобы не путать с основным компонентом.

```
.
└── src
    └── projects
        └── hotels
            └── components
                └── BookInfo
                    └── BookInfo.tsx
                    └── BookInfoContainer.tsx
```

## Вспомогательные функции

### Общие функции

Лежат в папках `utilities`. Если предполагается, что функций будет достаточно много, то рекомендуется группировать в подпапки по смыслу.

Общие для всего проекта функции лежат в папке `/src/utilities`.

```
.
└── src
    └── utilities
        └── getNow.ts
```

Сгруппированные по смыслу.

```
.
└── src
    └── utilities
        └── strings
            └── capitalizeFirstLetter.ts
            └── charCodes.ts
            └── humanList.ts
            └── lowercaseFirstLetter.ts
```

### Функции вертикалей

Специфичные для вертикалей функции лежат в папках `/src/projects/<projectName>/utilities`.

```
.
└── src
    └── projects
        └── hotels
            └── time
                └── calculateTotalNights.ts
```

### Функции React компонентов

Если функция является достаточно специфичной и с большой долей вероятности будет использоваться в рамках какого-то одного компонента, то функция должна лежать рядом с компонентом.

```
.
└── src
    └── components
        └── Button
            └── Button.tsx
            └── utilities
                └── calculateSmth.ts
```

### Прочие функции

Любые другие вспомогательные функции должны лежать в папке `utilities` сущности, в которой они используются.
