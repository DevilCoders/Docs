# 

Общие компоненты

## Состав пакета и roadmap
TBD

## Установка пакета
TBD

## Разработка
TBD

### Подготовка
TBD

### Структура компонента

Для нового компонента создайте директорию c его именем в _src/components_.
Чтобы избежать необходимости импортировать такие компоненты:
```
import { Button } from './Button/Button'
```
создавать файл index.tsx в той папке компонентов, которая экспортирует именованный компонент.
```
export * from './Button'
```

```
src/components/Block
├── Button.css
├── Button.tsx
├── index.tsx
└── _theme — Модификатор
    ├── Button_theme_night.css
    └── Button_theme_night.tsx
```
