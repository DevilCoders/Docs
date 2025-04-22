# Локальные дополнения к библиотеке torch_lib

Дополнения обычно задаются в файлах
- `feature_sets.py`
- `target_transforms.py`
- `features_transforms.py`

которые могут находиться как внутри директории torch_lib, так и снаружи.

В последнем случае ппредполагается, что файлы используютсся и как обычные python 
исходные файлы.

## Feature sets

В файле `feature_sets.py` должны определятся словари
- `flt_feature_sets`
- `cat_feature_sets`
- `super_feature_sets`

## Target transforms

В файле `target_transforms.py` должен определятся словарь `target_transforms`,
специфичный для данного проекта

## Features transforms

В файле `features_transforms.py` должен определятся словарь `features_transforms`
