# Logo as a Service

Генератор логотипов. Создает логотипы сервисов, набранные фирменным шрифтом Яндекса (доступно два формата: `SVG` и `PNG`).

![](https://yastatic.net/q/logoaas/v1/Яндекс.Логотип.svg)

Чтобы сгенерировать логотип, достаточно запросить файл https://yastatic.net/q/logoaas/v1/Логотип.svg или https://yastatic.net/q/logoaas/v1/Логотип.png, где слово «Логотип» заменить на необходимое вам.

> **Примечание.** Поддерживаются русский, английский, украинский, французский и турецкий алфавиты.

С более подробной документацией можно ознакомиться в <a href='https://github.yandex-team.ru/soft/logoaas' target="_blank">репозитории<a/> сервиса.

## Пример использования

```ts
import React from 'react'

const App = () => (
  <img
    src="https://yastatic.net/q/logoaas/v1/Яндекс.Сервис.svg"
    alt="Яндекс.Сервис"
  />
)
```
