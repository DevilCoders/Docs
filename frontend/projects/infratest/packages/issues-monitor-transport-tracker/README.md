# issues-monitor-transport-tracker

Транспорт Трекера для пакета `issues-monitor-cli`.

Создаёт тикет по шаблону из секции `tracker`.

Пример использования (несущественные части опущены):

```bash
issues-monitor -p template-settings.json -t tracker […]
```

Поддерживается [EJS v1](https://github.com/tj/ejs) шаблонизация полей `summary` и `description` из файла, если указать объект со свойством `template` с именем файла (без расширения `.ejs`) внутри директории `templates` пакета `@yandex-int/si.ci.ejs`:

```json
[
  {
    "transport": "tracker",
    "issueSummary": { "template": "my-template.summary" },
    "issueDescription": { "template": "my-template.description" }
  }
]
```

`@yandex-int/si.ci.ejs/templates/my-template.summary.ejs`:

```html
Всё пропало в <%= projectName %>
```

`@yandex-int/si.ci.ejs/templates/my-template.description.ejs`:

```html
См. задачи <%= issues.map((i) => i.key).join(', ') %>
```

Внутри шаблона доступны следующие данные:

* `projectName` — оригинальное значение опции `--project`;
* `query` — оригинальное значение опции `-q, --query`;
* `issues` — найденные по запросу `query` задачи в виде объектов формата `Startrek.Issue`, как их отдаёт Tracker API;
* `issueStatusKey` — оригинальное значение опции `-s, --issue-status-key`;
* `users` — логины пользователей, полученные после разбора опции `--recipients`.
