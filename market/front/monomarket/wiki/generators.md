Пакеты генераторы
===============

Чтобы настроить генератор нужно проделать следующее:

- создать директорию куда будет собираться итоговый генерируемый пакет
- добавить содержимое этой директории в `.gitignore`, исключая `package.json` Например:

```gitignore
dist/*
!dist/package.json
```

- скопировать `package.json` в директорию сборки
- в исходном `package.json` выставить флаг `private: true`.
- в исходном `package.json` изменить имя пакета, например дописать суффикс `-src`
- в исходном `package.json` добавить конфиг в формате:

```json
{
  "config": {
    "generate": {
      "target": "npm-package-name",
      "dist": "./path/to/dist/dir"
    }
  }
}
```

- в скопированном `package.json` добавить кофиг в формате:

```json
{
  "config": {
    "generator": "npm-package-name-src"
  }
}
```

- запустить `yammy validate generators fix`
