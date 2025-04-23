# @ps-int/boilerplate

Пакет-бойлерплейт для создания новых пакетов. Реализует все наши соглашения по требованиям к пакетам.

В комплекте:
- typescript
- линтер (`@ps-int/ps-lint`)
- прекоммитный линтер
- тесты (`jest`)
- транспиляция в js с генерацией декларациий типов
- изоморфная публикация `npm run package {{version}}`/`npm version {{version}} && npm publish`
- вспомогательные файлы
  - gitignore
  - eslintignore
  - editorconfg
  - npmrc
  - nvmrc

## Как использовать?
- придумать имя пакета (для примера возьмём имя `kotik`)
- скопировать в `packages/kotik` содержимое `packages/boilerplate`
- заменить поле `name` в `packages/kotik/package.json` на `@ps-int/kotik`
- `npm ci`
- писать код в `lib`
- `npm run package 1.0.0` опубликует ваш первый мажор Котика

Наслаждайтесь!

## TODO

Сборка для пакетов, требующих поставки в виде бандла.
