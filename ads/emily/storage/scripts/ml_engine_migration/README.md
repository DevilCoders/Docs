# ML_ENGINE_DUMP -> ML_STORAGE_DUMP migration script

Скрипт перекладывает модели формата ML_ENGINE_DUMP в формат ML_STORAGE_DUMP.

```bash
ya make -r
./migrate --help
```

### Вариант 1

Передать ML_ENGINE_DUMP Sandbox resource id через --sbr

```bash
./migrate --sbr 2550323380
```

Можно передать несколько ML_ENGINE_DUMP Sandbox resource id через --sbr id1 --sbr id2 т.д.
Для каждой модели скрипт запросит желаемое название (ключ), версию
(дата в формате %Y-%m-%dT%H%M%S, пример: 2022-01-01T00:00:00) и владельца будущей модели в MLStorage.

### Вариант 2

Также модели можно передать через yaml файл указав для каждой
sbr (ML_ENGINE_DUMP Sandbox resource id), name, version, owner
(см. ads/emily/storage/scripts/ml_engine_migration/models.yaml).

```bash
./migrate -f models.yaml
```

После этого модели будут скачаны в директорию --download-dir (default: ./models/)
(если не пуста после вопроса y/n будет очищена),
конвертированы в соответствующий формат и загружены MLStorage.
Информация по загруженным моделям появится в --output (default: ./uploaded_models.yaml)
