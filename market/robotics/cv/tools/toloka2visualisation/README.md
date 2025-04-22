# Toloka 2 Visualisation

Утилита визуализирует разметку (из tsv файла) с Толоки и сохраняет изображения в указанную папку.

## Пример использования:

```shell
./toloka2visualisation --file labeling_0522.tsv --save-folder ./visualisation
```

Файлы сохраняются в формате `{id}_{system:itemId}.jpeg` в указанную папку.
