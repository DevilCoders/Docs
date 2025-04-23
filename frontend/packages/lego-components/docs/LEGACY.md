# Архитектура

Архитектура библиотеки `@yandex-lego/components` ориентирована на разделение компонентов на небольшие, независимые и легко изменяемые части.

## Соглашение по именованию

- Все компоненты именуются согласно [React-стилю](https://ru.bem.info/methodology/naming-convention/#Стиль-react).
- Все уровни переопределения находятся в директории компонента и разделяются (за исключением уровня `common`) через знак `@`:

    Синтаксис: `Button@<platform>.<tech-name>`.

    Пример: `Button@desktop.tsx`.

## Cтек технологий

В Лего используются следующие технологии:

- [TypeScript](https://www.typescriptlang.org)
- [PostCSS](https://postcss.org)
- [bem-react](https://github.com/bem/bem-react)

## Структура компонента

Все компоненты имеют схожую файловую структуру.

Пример:

```bash
src/Button
├── Text                        # Элемент
│   ├── Button-Text.css
│   └── Button-Text.tsx
├── _view                       # Модификатор
│   ├── Button_view_default.css
│   └── Button_view_default.tsx
├── Button.tests
│   ├── Hermione.components
│   ├── Button.hermione.js      # Hermione-тесты
│   └── Hermione.tsx            # Страница с примерами для тестов
├── Button.registry
│   ├── interface.ts            # Интерфейс реестра
│   └── desktop.ts              # Реестр зависимостей для Desktop-платформы
├── Button.css                  # Стили
├── Button.test.ts              # Unit-тесты
├── Button.tsx                  # Common-реализация
└── Button@desktop.tsx          # Desktop-реализация
```
