Данный скрипт вычисляет модель для сравнения скриншотов с коллекцией.

Запуск:   
1. Убедиться, что модуль screenqual доступен в python path. Например, достаточно положить его рядом с model_generators и добавить в PYTHONPATH путь "..".   
2. Запустить из директории model_generators скрипт
```PYTHON_PATH=. python similarity_checker_model_generator.py absolute_path_to_collection file_extension_preceeded_with_dot```

Результат: файлы со средним спектром коллеции и с индексами, необходимыми для сравнения, предлагаемое значение порога.

Известные проблемы:
1. предлагаемое значение порога может быть завышенным, что приведёт к увеличению количества FN.
Предлагается провести эксперименты на большой коллекции для точного определения порога.