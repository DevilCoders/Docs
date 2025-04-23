# Интеграция с webstorm
Webstorm не имеет интеграции с lerna, но его можно настроить для запуска и дебага тестов.

## Работа ESLint
По умолчанию интеграция с ESLint не работает с монорепозиториями, в которых сам линтер (`eslint`) установлен в каждом пакете, а не в корневом `package.json`. Эту поддержку нужно включать вручную.

Нужно перейти к настройкам ESLint:

```
Preferences → Languages & Frameworks → JavaScript → Code Quality Tools → ESLint
```

В поле `Extra eslint options` добавить значение:

```
--resolve-plugins-relative-to ./node_modules/@yandex-int/eslint-config-infratest
```

## Индексация проекта
Webstorm плохо индексирует рекурсивные симлинки, поэтому их нужно исключить из проекта. На данный момент такая симлинка одна -
`packages/archon-renderer-devserver-command/test/fixtures/test-project/node_modules`. Нужно пометить эту папку исключенной из
проекта и webstorm не будет индексировать ее содержимое.
![exclude symlinks](./assets/exclude_symlink.png)

Индексация всего проекта с нуля, включая все node_modules, занимает не более минуты на ноутбуке с ssd (обычно - половину минуты).

## Запуск тестов из IDE
Интеграция с тестовыми фреймворками начинает работать только после полной индексации проекта.

Эта интеграция не работает в power save mode - убедитесь, что режим сбережения энергии выключен.

Для JS-пакетов тесты запускаются при помощи mocha, IDE все корректно определяет:
![running tests](./assets/run_tests.png)

В TS-пакетах тесты запускаются при помощи jest. Есть два разных конфига для тестов - для unit-тестов и для функциональных тестов.

Unit-тесты запускаются без лишних манипуляций:
![running tests in TS](./assets/run_test_ts.png)

Функциональные тесты не запустятся: `No tests found, exiting with code 1`. Чтобы это исправить, нужно в созданную конфигурацию запуска прописать путь до конфига с функциональными тестами: `-c ./jest.config.func.js`

![running func tests in TS](./assets/run_func_test_ts.png)

Тесты можно запускать в режиме дебага с брейкпоинтами, просмотром переменных и прочими радостями.

## Оставить только нужные проекты

Это делать не обязательно, станет немного удобнее при долгой работе над ограниченным числом проектов.

Зайти в настройки (`cmd + ,` в macos) -> directories, удалить `content root`:
![content root](./assets/preferences.png)

Добавить в content root все проекты из папки packages, это можно сделать за один раз:
![all roots](./assets/content_root.png)

При настроенных проектах работает резолв имен от корня проектов, используемый в тестах. Например, https://github.yandex-team.ru/search-interfaces/infratest/blob/846fbbf04d47405d758d4b63578e351530a1da06/packages/gui-assistant/test/lib/plugin.js#L7
