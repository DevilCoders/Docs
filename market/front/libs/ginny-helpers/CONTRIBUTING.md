# Разработка

  Для разработки нужны `node >= 8.9` и `git`.

## Клонирование

  ```sh
  git clone https://github.yandex-team.ru/uid11/ginny-helpers.git
  cd ginny-helpers
  ```

## Настройка окружения

- Установка зависимостей:

  ```sh
  npm install
  ```

- Установка `peer`-зависимостей (обязательна для разработки):

  ```sh
  npm run bootstrap
  ```

## Проверки

- `flow`-типизация и кодстайл:

  ```sh
  npm run lint
  ```

- Только `flow`-типизация:

  ```sh
  npm run lint:flow
  ```

- Вывод не только ошибок, но и всех `warning`-ов от `flow`:

  ```sh
  npm run lint:flow-include-warnings
  ```

- Вывод всех лишних подавлений ошибок `flow`:

  ```sh
  npm run lint:flow-unused-suppression
  ```

- Только кодстайл:

  ```sh
  npm run lint:js
  ```

- Тесты:

  ```sh
  npm test
  ```

- Покрытие типами `flow` и тестами:

  ```sh
  npm run coverage
  ```

- Покрытие только типами `flow`:

  ```sh
  npm run coverage:flow
  ```

  Отчёт сформируется в файле `flow-coverage/index.html`.

- Покрытие только тестами:

  ```sh
  npm run coverage:test
  ```

  Отчёт сформируется в файле `coverage/index.html`.

## Релиз

  Если выполнена авторизация на `npm.yandex-team.ru`, и `npm`-пользователь добавлен во владельцы пакета
  (`npm owner add username ginny-helpers`), релиз можно собрать и опубликовать командой

  ```sh
  npm version {major|minor|patch}
  ```
  `CHANGELOG.md` и плашки из `README.md` обновятся автоматически.
