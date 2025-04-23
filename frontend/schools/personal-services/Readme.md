# Фронтенд Яндекс 360

Школа фронтенда Яндекс 360 (Персональные сервисы).

## Технологии

### Рекомендованные зависимости
||||
|-|-|-|
|Язык|[`typescript`](https://www.npmjs.com/package/typescript)|^4.5.0|
|UI|[`react`](https://www.npmjs.com/package/react)|^16.14.0|
||[`react-redux`](https://www.npmjs.com/package/react-redux)|^7.2.2|
|State|[`redux`](https://www.npmjs.com/package/redux)|^4.0.3|
||[`redux-saga`](https://www.npmjs.com/package/redux-saga)|^1.1.0|
|Routing|[`react-router-dom`](https://www.npmjs.com/package/react-router-dom)|^5.2.0|
|Сборка|[`@ps-int/ps-build`](../../../yandex360/frontend/packages/ps-build)|^4.0.1|
|Unit-тесты|[`jest`](https://www.npmjs.com/package/jest)|^27.2.4|
|Линтер|[`@ps-int/ps-lint`](../../../yandex360/frontend/packages/ps-lint)|^3.2.0|
|Дизайн-система|[`@yandex-lego/components`](https://lego.yandex-team.ru/lego-components/)|^3.26.0|
||[`@ps-int/mg-theme`](../../../yandex360/frontend/packages/mg-theme)|^2.0.2|
|Локализация|[`@ps-int/ps-tanker`](../../../yandex360/frontend/packages/ps-tanker)|^1.2.0|
|RUM-скорость|[`@yandex-int/rum-counter`](https://a.yandex-team.ru/arc_vcs/frontend/packages/rum-counter)|^4.7.0|

## Сервисы

### Скрипты

Каждый сервис должен иметь минимальный единообразный набор npm-скриптов на уровне **корня** проекта
|||
|-|-|
|`start`|Запуск сервиса для разработки|
|`test`|Запуск "быстрых" тестов, скорее всего модульных, для проверки во время разработки|
|`lint`|Запуск линтеров во всех частях сервиса|
|`setup`|Подготовка сервиса к первому запуску (Если требуется)|
|`package`|Сборка пакета|
|`deploy`|Выпуск релиза|
|`ci:test`|Запуск полного набора тестов в CI|
|`ci:lint`|Запуск линтеров в CI|
|`ci:build`|Сборка сервиса для деплоя в продакшн-режиме|
|`ci:publish`|Публикация собранных артефактов сервиса|

### Языки
|||
|-|-|
|Код|✅ `typescript`|
||❌ Не рекомендуется использование чистого ~~JavaScript~~'а|
|Стили|✅ CSS-модули + autoprefixer|
||❌ Не рекомендуется использование препроцессоров, таких как ~~`stylus`~~ или ~~`sass`~~|

### Cборка и деплой
|||
|-|-|
|Сборка или транспиляция|✅ `@ps-int/ps-build`|
||❌ Не рекомендуется использование ~~`webpack`~~ или ~~`tsc`~~ напрямую|

Пакет `@ps-int/ps-build` предоставляет следующие скрипты
|||
|-|-|
|`ps-build`|Сборка webpack'ом|
|`ps-transpile`|Транспиляция через `tsc`|
|`ps-upload-static`|Загрузка статики проекта в s3|
|`ps-clear-static`|Удаление загруженной статики из s3|

> TODO: сделать общий инструмент для сборки ресурса и работы с deploy'ем

### Стиль кода
|||
|-|-|
|Линтер|✅ `@ps-int/ps-lint`|
||❌ Не рекомендуется использование ~~`eslint`~~ или ~~`lint-staged`~~ напрямую|

Пакет `@ps-int/ps-lint` предоставляет следующие скрипты
|||
|-|-|
|`ps-lint`|Проверяет code-style во всём проекте с помощью `eslint`|
|`ps-lint-staged`|Проверяет code-style в staged-файлах с помощью `lint-staged`|

> Ключи в танкере заводятся строго в camelCase, если ключ не содержит разметки и в PascalCase, если ключ содержит разметку — такой ключ будет скомпилирован в react-компонент

### Unit-тесты
> TODO: сделать общий пакет `@ps-int/ps-test`

Используем `jest` + `babel-jest` и конфигурацию, основанную на babel-пресете `ps-build`'а
```javascript
// jest.config.js
module.exports = {
    transform: {
        '\\.[jt]sx?$': ['babel-jest', {
            configFile: './node_modules/@ps-int/ps-build/lib/babel/babel.config.js',
        }],
    }
};
```

### Вспомогательные библиотеки
|||
|-|-|
|Вспомогательные функции|✅ `lodash-es`|
||❌ Не рекомендуется использовать обычную сборку ~~`lodash`~~|

> TODO: выбрать библиотеку для работы с датами — `moment` / `luxon` / `date-fns`

### Локализация
|||
|-|-|
|Работа с Танкером|✅ `@ps-int/ps-tanker`|
||❌ Не рекомендуется использовать ~~`react-tanker`~~ и утилиту ~~`git tanker get`~~|

Для локализации используется пакет `@ps-int/ps-tanker`, он предоставляет скрипты
|||
|-|-|
|`ps-tanker`|Точка входа, предложит создать конфигурацию или выполнить одну из команд|
|`ps-tanker update`|Обновить ключи из Танкера|
|`ps-tanker config`|Настроить проект|

> Подробнее можно прочитать в [репозитории ps-tanker](../../../yandex360/frontend/packages/ps-tanker)

### RUM
|||
|-|-|
|Метрики скорости|✅ `@yandex-int/rum-counter` — [Инструкция по использованию](https://wiki.yandex-team.ru/velocity/rum/)|
|Пользовательские события|Яндекс.Метрика|

> TODO: библиотека для работы с Метрикой

### Дизайн-система
|||
|-|-|
|Компоненты|✅ `@yandex-lego/components` версии 3 |
||❌ Не рекомендуется использовать ~~`lego-on-react`~~ или ~~`@yandex-lego/components` версии 2 и ниже~~|
|Тема Лего|✅ `@ps-int/mg-theme`|
