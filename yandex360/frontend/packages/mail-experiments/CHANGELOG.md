# Changelog

All notable changes to this project will be documented in this file.

## 2.0

### Breaking Changes

`set()` принимает только два аргумента:
* первым — ответ модели `experiments` в новом формате (`{ ExpBoxes: string, Handlers: Handler[]}`)
* вторым — объект данных пользователя (не нужно конвертировать в `Map`).

Рекомендуется использовать с [@duffman-int/service-user-split](../@duffman-int/service-user-split)
