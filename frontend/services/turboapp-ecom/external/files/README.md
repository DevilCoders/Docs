# @yandex/tap-ecom

Шаблон для быстрого старта разработки интернет-магазина для [платформы турбо-сервисов Яндекса](https://yandex.ru/dev/turboapps/doc/concepts/index-docpage/). Предоставляет готовый фронтенд для интернет-магазина, оставляет возможность глубокой кастомизации.

Манифест демо-магазина: `https://ecom.tap.yandex.net/manifest.json`

[Инструкция по установке манифеста](https://yandex.ru/dev/turboapps/doc/dev/testing-docpage/) в Яндекс.Браузер.

Шаблон содержит:
- Набор сверстанных экранов для стандартного интернет-магазина, таких, как: главная, каталог, страница товара, корзины и тд.
- Готовый слой работы с данными, поддерживающий работу в оффлайн.
- Простой способ подключения API любого интернет-магазина.
- Интеграцию с возможностями платформы турбо-сервисов.
- Сборку веб-приложения, оптимизированную для платформы турбо-сервисов.

## Как создать магазин на основе шаблона?

1. Скопировать код шаблона в свой проект.
2. Реализовать и подключить [модуль API](./README.md#модуль-api) для работы с бекендом вашего магазина.
3. Прописать `clientId` и `metrikaId` в файле `./src/config.json`.
4. [Кастомизировать проект](./README.md#кастомизация) (опционально).
5. Зарегистрироваться в [кабинете разработчика](https://yandex.ru/dev/turboapps/doc/admin-panel/registration-docpage/) и пройти [модерацию](https://yandex.ru/dev/turboapps/doc/admin-panel/review-docpage/).

## Технологии

В шаблоне используются:
- [TypeScript](https://www.typescriptlang.org/) – весь код строго типизирован, что упрощает кастомизацию и поддержку.
- [React](https://reactjs.org/) – стандарт де-факто для разработки SPA веб-сервисов.
- [Redux](https://redux-toolkit.js.org/) – для управления состоянием и работы в оффлайн.
- [tap-components](https://github.com/yandex/tap-components) – библиотека react-компонентов для турбо-сервисов.
- [tap-scripts](https://github.com/yandex/tap-scripts) – конфигурация для сборки турбо-сервисов.
- [tap-js-api](https://github.com/yandex/tap-js-api) – TypeScript-адаптеры для JS API платформы турбо-сервисов.


## Документация

- Документация по [React](https://reactjs.org/).
- Документация по библиотеке компонентов  [tap-components](https://github.com/yandex/tap-components).
- Документация по сборке через  [tap-scripts](https://github.com/yandex/tap-scripts).
- Документация по [JS API платформы турбо-сервисов](https://yandex.ru/dev/turboapps/doc/api/about-docpage/) и [TypeScript-адаптеру для JS API](https://github.com/yandex/tap-js-api)
- [Подробнее про Redux в шаблоне](./src/redux/README.md)


## Запуск

1. Установить зависимости

```bash
npm ci
```

2. Запустить турбо-сервис для локальной разработки

```bash
npm start
```

3. Открыть турбо-сервис по ссылке [http://localhost:3000](http://localhost:3000).


## Команды

-   `npm start` – запуск в режиме разработки
-   `npm run build` – сборка production версии


## Типы данных

Типы данных, используемые в шаблоне, хранятся в пакете `@yandex/tap-ecom-types`.
- [Описание типов данных](https://github.com/yandex/tap-ecom-types/tree/master/src/data)

## Модуль API

Для загрузки данных с сервера шаблон использует специальный модуль API, который должен экспортироваться из файла `./src/api.ts` и иметь тип `Api` из `@yandex/tap-ecom-types`.
Для того, чтобы интегрировать шаблон с конкретным интернет-магазином, нужно реализовать собственный модуль API.

- [Описание модуля API](https://github.com/yandex/tap-ecom-types/tree/master/src/api/docs)
- [Пример модуля с моками](https://github.com/yandex/tap-ecom-mocks-api/blob/master/src/index.ts) – можно взять за основу

## Компоненты

Шаблон использует библиотеку компонентов `@yandex/tap-components`. Из готовых компонентов можно разработать дополнительные экраны и функциональность для вашего интернет-магазина.
- [Документация и примеры](https://github.com/yandex/tap-components)

## Кастомизация

### Кастомизация стилей

Общие настройки стилей расположены в файлах `./src/constants/ui`. С помощью CSS-переменных можно задать основные цвета, стили кнопок и текстов.
Также может быть настроено отображение многих компонентов из библиотеки `@yandex/tap-components`.

### Кастомизация экранов

Состав блоков на экране может быть изменен в директории `./src/screens`.

Поменять url-адрес экрана можно в файле `./src/app.tsx`, после этого нужно также поменять логику генерации ссылок в файле `./src/libs/url-manager.ts`.

### Добавление новых экранов

Для добавления экрана нужно:

1. Создать компонент экрана в папке `./src/screens`, можно использовать готовые компоненты из библиотеки `@yandex/tap-components`.
2. Подключить экран в файле `./src/app.tsx`.
3. Подключить экран к данным в Redux. При необходимости, добавить новые методы работы с сервером в модуль API.


## Список доработок

Планируемые изменения в шаблоне:

- Новая функциональность
    - Поиск
    - Фильтрация товаров в категориях
    - Переключатель тематики магазина (глобальный фильтр). Например, "Женщинам" / "Мужчинам"
- Лоадеры на время загрузки кода в экранах
- Верстка большинства экранов будет перенесена из шаблона в библиотеку `@yandex/tap-components`
- Больше документации и упрощение работы с Redux

