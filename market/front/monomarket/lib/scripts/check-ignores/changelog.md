# 1.0.0

**PR:** [#2505309](https://a.yandex-team.ru/review/2505309)
**Author:** @gheljenor **Date:** 2022-04-27

[undefined](https://st.yandex-team.ru/undefined) - undefined

Новая утилита для валидации и синхронизации состояния arcignore и gitignore файлов. Для синхронизации считает источником истины файл игнора относящийся к текущей vcs-системе.

### Usage

```shell
yammy bin check-ignores check [files..] # для проверки
yammy bin check-ignores fix [files..] # для автоматического исправления
```

Если не передавать список файлов, будут проверены/исправлены все файлы gitignore/arcignore в монорепе

### Migration

Первая версия