# Конвертер данных в тестовую выборку

Утилита позволяет получить JSON c разметкой и изображения из url разметки, сложив в заданную папку

## Пример запуска
```shell
./toloka2test --pattern "/Users/ilinvalery/Developer/plt_detector/dataset_to_yt/realdata/test/*.tsv" --folder-name ./pltqr_test --out pltqr_test.json --ignore-pattern "/Users/ilinvalery/Developer/plt_detector/dataset_to_yt/ignored/*.tsv"
```

Результат скрипта:
1. Изображения в папке `./pltqr_test`;
2. JSON разметка в файле `pltqr_test.json`
