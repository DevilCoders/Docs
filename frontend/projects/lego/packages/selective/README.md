# selective

## selective configure

Определяет все затронутые в PR блоки через [обратные зависимости](https://github.com/zxqfox/gather-reverse-deps) и выводит результат в JSON-формате в консоль.

### Пример запуска

```bash
$ selective configure
```

### Пример вывода в консоль

```json
{
  "specialFileTypes": [],
    "FULL":  {
      "entities": ["check-button", "auth", "user", "user__enter"],
      "blocks": ["check-button", "auth", "user"]
    }
}
```

## selective transform

Этот хелпер использует результаты запуска `selective configure` и преобразует их в удобный формат для передачи полученного списка в тест-утилиту, например, `hermione`.

### CLI

* `--file=<filename>` – файл, в котором находится результат запуска `selective configure`
* `--target=<blocks|entities|tmpl-specs|docs|examples>`
* `--platform=<desktop|touch-pad|touch-phone>` – платформа; несколько платформ передается через запятую
* `--separator=<separator>`

### Пример запуска

```bash
$ selective transform --file=selective.json --target=hermione --platform=desktop --separator="|"
```
