## Структура проекта

```bash
  CORE
  ├── components // содержит переиспользуемые компоненты приложения, которые можно добавлять на страницы. Стили, типы, неймспейсы, уникальные фото и т.д. храним в  папке отдельного компонента
  │   └── Component
  │       ├── index.tsx
  │       ├── Component.test.tsx
  │       └── asset.png
  ├── content // содержит статический контент для отображения на страницах (вопрос WIP)
  │   ├── news
  │   │   └── frontend-news.mdx
  │   ├── people
  │   ├── quotes
  │   ├── vacancies
  ├── docs // содержит документацию по проекту
  │   └── CODE_STRUCTURE.md
  ├── hocs // здесь храним хоки для всего проекта, а они обязательно появятся
  ├── pages // страницы приложения
  │   ├── mainPage
  │   ├── vacancyAllPage
  │   ├── vacancyPersonalPage
  │   ├── vacancyBenefitsPage
  │   └── vacancyInterviewPage
  ├── public // здесь хранятся общие для всего приложения шрифты и фото
  │   ├── fonts
  │   └── img
  └── ui // UI-kit приложения
      └── element
          ├── ui-element.tsx
          └── index.ts
```
