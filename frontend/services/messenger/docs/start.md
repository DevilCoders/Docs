# Быстрый старт

## Подготовка окружения

Мы рекомендуем использовать [nvm](https://github.com/creationix/nvm) для управления версиями node.js. Установите `nvm` перед началом работы

Разработка ведется в системе arc, поэтому сначала необходимо установить [arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

После монтирования хранилища arc, необходимо собрать проект:
```bash
cd {arc_path}/frontend
npm i
cd services/messenger
nvm use
npm i
npm run build
```

Настройте свой редактор кода на использование `typescript` ([TypeScript Editor Support](https://github.com/Microsoft/TypeScript/wiki/TypeScript-Editor-Support)) и `eslint` — они подскажут ошибки и будет доступен удобный code autocomplete.

## Команды для локальной разработки и сборки

В качестве локального сервера мы используем [kotik](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/kotik) (пришёл на смену templar), который запускается через [archon](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon)

- `npm start` — запуск kotik командой archon (с туннелем до публичного хоста).
- `make build` — сборка проекта для production.
- `npm test` — запуск Unit-тестов.

## [Как использвать arc](https://docs.yandex-team.ru/devtools/src/arc/workflow)

Основная информация использования arc описана в документации.

Ветки создаем с названием `{feature-name}.{TASK-NUMBER | TRIVIAL}`. TRIVIAL являются ПР без задач. 
Такими могут быть минорные изменения документации или подобные

## Сборки

Основной адрес:
- https://{nickname}-1-ws1.tunneler-si.yandex{-team}.ru — публичный адрес котика при запуска котика.


Остальные
- https://local.yandex.ru:3443 — адрес котика по умолчанию в чатах.
- http://localhost:3333 — локальный адрес котика (порт можно поменять при запуске котика с флагом --port).
- https://renderer-chat-pull-NNNN.hamster.yandex.ru — адрес из PR (по ссылкам из описания PR).

## Виджет

Сам виджет находится в отдельном сервисе: `{arc_path}/frontend/services/messenger.widget_deprecated`, 
но запускать можно и из репозитория мессенджера. Для этого необходимо установить модули в репозитории виджета `npm i`

После чего при запуске локальной сборки можно пройти по ссылке `https://{nickname}-1-ws1.tunneler-si.yandex{-team}.ru/widget`,
где будет запущен стенд виджета


## Подробнее про TypeScript

Ещё раз ссылка на [официальный сайт](https://www.typescriptlang.org/).
Можно прочитать серию статей от нашего коллеги [@mrmlnc](https://staff.yandex-team.ru/mrmlnc):

  1. [TypeScript: Введение](https://canonium.com/articles/typescript-introduction)
  2. [TypeScript: Типы и Структуры](https://canonium.com/articles/typescript-types-and-structures)
  3. [TypeScript: Обобщённые типы (Generics)](https://canonium.com/articles/typescript-generics)
