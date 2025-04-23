# @yandex-int/stub-components

Stub для создания пакета с компонентами на React

## Основные команды

`npm start` - запускает storybook

`npm run build:storybook` - собирает storybook

`npm run build` - собирает компоненты

## Создание своего пакета

Чтобы создать свой пакет с компонентами, вам нужно выполнить несколько простых шагов:

1. Запустить `npm run create-leaf` в директории `frontend`.
2. Выбрать `package-components`.
3. Ввести название пакета, например: `lego-components`.

## Используемые технологии

Подготовлена инфраструктура для написания компонентов на React с TypeScript.
Для создания различных примеров компонентов служит сторибук.
При создании/обновлении PR сторибук автоматически публикуется в s3 по пути `https://frontend-test.s3.mds.yandex.net/story/@yandex-int/<name-components>/pull-<pr-number>/index.html`.
После влития PR, бакет автоматически очищается.
Для тестирования используется `jest` и `hermione`.
