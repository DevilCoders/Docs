Cорцы в intranet/wiki/devtools/yamake_prep

Использование
```
yamake_prep input_file output_file
```

Общий формат макроса (все очень примитивно, не хотелось тащить парсер)

```
%отступ $$%ИМЯ_МАКРОСА% %JSON_С_АРГУМЕНТАМИ%
```

Макросы которые сейчас есть

```
$$WARN {}
```

раскрыть в предупреждение о том, что файл автосгенерён

```
$$GLOB {"pattern": ["wiki/**/*.py"]}
```

раскрыть в то что попадет в glob от папки где будет лежать output_file (формат шаблонов такой же как в гитигноре). При этом сохраняется порядок файлов отсортированный по алфавиту (сначала папки - затем файлы) чтобы были красивые диффы

```
$$PY_MODULE {"rel_path": "wiki", "match": "^((.*?)\\.management).*", "replace": "\\g<1>.*"}
```

пройти в папке где будет лежать output_file рекурсивно и выполнить замену. Я их сделал чтобы прописать в игнор тестов на импорт джанговские миграции
