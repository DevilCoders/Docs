# Как обновить разделы документации

Чтобы обновить или добавить новые разделы документации в список контента (Table of Content) необходимо отредактировать файл [toc.yaml](https://a.yandex-team.ru/arc_vcs/noc/docs/nocdocs/toc.yaml).

Подробная документация по обновлению структуры находится в [официальном гайде по документации](https://docs.yandex-team.ru/docstools/settings/toc)

Вы можете добавить новый раздел добавив операнд `name` в соответствующий целевому разделу `items`:
```
  - name: Начало работы
    href: index.md
```

`href` - путь до файла в проекте – относительный (например, `./drills/manuals/drill/about.md`) или урл (например, `https://docs.yandex-team.ru/nocrfcsd/`)
