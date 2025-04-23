# YANG pool result To Toloka Labeling TSV file

Данная утилита позволяет сконвертировать файл разметки из YANG в TSV формат Toloka Ready-To-Go

После сборки через систему `ya make` выполнить следующую команду:

```shell
./yangpool2toloka --file output_100622.json --out labeling_gt_100622.tsv [ --key-phrase ride_right_forward]
```

Где

- `--file` - файл для обработки
- `--out` - tsv итоговый файл
- `--key-phrase` - ключевая фраза в URL (полезно для разбивки на конкретные батчи, параметр не обязателен)
