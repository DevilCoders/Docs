# Компоненты

Все компоненты реализуются на [React](https://reactjs.org). Вдохновение можно искать [тут](https://github.com/brillout/awesome-react-components).

Большинство компонентов реализуется с использованием пакетов: [@bem-react](https://github.com/bem/bem-react). Но это не является обязательным условием к реализации компонента. Видео-презентация `@bem-react/*` доступна [тут](https://youtu.be/pVzlkCidOYg).

Компоненты для нескольких платформ разрабатываются с помощью [@bem-react/di](https://www.npmjs.com/package/@bem-react/di)

Структура компонентов:

* 📁 — всегда папка
* 📄 — всегда файл
* 📄/📁 — папка или файл
* 📤 — Экспортируемые сущности
* ⛔ — Больше ничего не должно экспортироваться

```
src/components
├──📁ComponentName
│   ├──📁_modName
│   │   ├──📄ComponentName_modName.tsx — простой модификатор
│   │   │   └── 📤 hoc withModName ⛔
│   │   ├──📄ComponentName_modName@platform.tsx — подключенный к registry
│   │   │   └── 📤 hoc withModName ⛔
│   │   ├──📄ComponentName_modName_modVal.tsx — модификатор со значением
│   │   │   └── 📤 hoc withModNameModVal ⛔
│   │   ├──📄ComponentName_modName_modVal@platform.tsx — подключенный к registry
│   │   │   └── 📤 hoc withModNameModVal ⛔
│   │   ├──📄ComponentName_modName_(modVal?)(@platform?).scss — стили
│   │   └──📄ComponentName_modName_(modVal?).typings.ts — тайпинги для модификатора
│   │
│   ├──📁ElementName
│   │   ├──📄ComponentName-ElementName.tsx — элемент блока ComponentName
│   │   │    └── 📤 class ComponentNameElementName ⛔
│   │   ├──📄ComponentName-ElementName@platform.ts — подключенный к registry
│   │   │    └── 📤 class ComponentNameElementName ⛔
│   │   └──📄ElementName(@platform?).scss — стили
│   │
│   ├──📁ComponentName.i18n — файлы переводов
│   │   ├──📄ru.ts — словарь для русского языка
│   │   ├──📄en.ts — словарь для английского языка
│   │   └──📄index.ts — словарь используемых языков
│   │
│   ├──📁ComponentName.assets — иконки, картинки
│   │
│   ├──📁ComponentName.test — все возможные тесты
│   │   ├──📄ComponentName.page-object.js — Page Object
│   │   ├──📄ComponentName.hermione.js — функциональный тест
│   │   └──📄ComponentName.spec.tsx — unit-тест
│   │
│   ├──📁ComponentName.registry — registry
│   │   └──📄platform.ts — registry для platform
│   │        └── 📤 class ComponentNameRegistry ⛔
│   │
│   ├──📄/📁ComponentName.typings(.ts) — тайпинги компонента
│   │   │                                если всё в одном файле — файл, если нет - папка
│   │   │
│   │   └──📄index.ts — экспортирует все типы из папки
│   │       ├── 📤 interface ComponentNameProps — свойства компонента
│   │       └── 📤 type ComponentNameType — тип компонента
│   │                   (Чтобы не писать везде ComponentType<ComponentNameProps>)
│   │
│   ├──📄/📁ComponentName.utils(.ts) — вспомогательные функции
│   │   │                              если всё в одном файле — файл, если нет - папка
│   │   │
│   │   └──📄index.ts — экспортирует все функции из папки
│   │
│   ├──📁ComponentName.hooks — хуки
│   │   ├──📄useHookName.ts - хук
│   │   │  └── 📤 function useHookName ⛔
│   │   └──📄index.ts — экспортирует все хуки из папки
│   │
│   ├──📄ComponentName.const.ts — константы использующиеся в компоненте
│   │
│   ├──📄ComponentName.tsx — компонент
│   │   └── 📤 class ComponentName ⛔
│   ├──📄ComponentName@patform.tsx — компонент подключенный к registry
│   │   └── 📤 class ComponentName ⛔
│   ├──📄ComponentName(@platform?).scss — стили
│   └──📄ComponentName.stories.tsx — примеры компонента для Storybook
│                                     загляни utils/storybook
```
