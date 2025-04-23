# Архитектура и стек технологий

## Соглашение по именованию компонентов

* Все компоненты должны быть названы согласно [react-naming](https://ru.bem.info/methodology/naming-convention/#Стиль-react)
* Все уровни переопределения находятся в одной директории и разделяются, за исключением `common` уровня, через знак `@` — `Button@<platform>.<tech-name>`

## Структура компонента

```
src/components/Button
├── Button.tests
│   ├── Hermione.components
│   ├── Button.hermione.js — Hermione тесты
│   └── Hermione.tsx — Страница с примерами для тестов
├── Button.registry
│   ├── interface.ts — Интерфейс реестра
│   └── desktop.ts — Реестр зависимостей для desktop платформы
├── Button.css — Стили
├── Button.test.ts — Unit тесты
├── Button.tsx — Common реализация
├── Button@desktop.tsx — Desktop реализация
├── Text — Элемент
│   ├── Button-Text.css
│   └── Button-Text.tsx
└── _view — Модификатор
    ├── Button_view_default.css
    └── Button_view_default.tsx
```
