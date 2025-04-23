# Инструмент для работы с конфигом аудиторий и сегментов

### add-audience
Добавить аудиторию

- `--partner-id` - какому партнеру принадлежит скор
- `--score-name` - имя скора
- `--low` - нижня граница
- `--high` - верхняя граница
- `--audience-name` - под каким именем будет залита аудитория, к имени будет добавлена граница аудитории с помощью `low` и `high`.
- `--parts` - на сколько сегментов разбить аудиторию
Необязательные
- `--export` - флаг, нужно ли экспортировать аудиторию в отдельную директорию
- `--export-folder` - имя директории для экспорта. Именно ИМЯ, путь предопределен

Пример
```
export AUDIENCE_TOKEN=""
./config add-audience --partner-id internal --score-name audience-1761 --low 0.9 --up 1.0 --audience-name audience_1761 --parts 5
```

Пример с экспортом
```
./config add-audience --partner-id internal --score-name audience-1761 --low 0.9 --up 1.0 --audience-name audience_1761 --parts 5 --export --export-folder export-1761
```

### delete-audience
Удалить аудиторию

- `--partner-id` - какому партнеру принадлежит скор
- `--score-name` - имя скора

Пример
```
./config delete-audience --partner-id internal --score-name audience-1234
```

### list-audience
Получить список аудиторий

- `--active` - только активные аудитории
- `--name-only` - вывести только имя аудитории

Пример
```
./config list-audience --active --name-only
```

### list-segments
Получить список сегментов в аудитории

- `--audience-name` - имя аудитории
- `--id-only` - вывести только id сегментов присвоенные я.аудиторией

Пример
```
./config list-segments --id-only --audience-name audience_1761_90-100
```
