# Реклама в Картах

## Эксперименты и extendConfig

При создании выборки для эксперимента, в конфиг выборки можно добавить особенный объект `extendConfig`, который позволит переписать поля в текущем конфиге продакшена, а так же, при необходимости, добавить в него новые значения.
Это может пригодиться, например, в случае обновления рекламных блоков в эксперименте.

Для того, чтобы добавить `extendConfig` в настройку выборки, нужно:

-   в массиве `pron` добавить дополнительное поле `extendConfig`

```
    "pron": [
        "extendConfig",
        "pron1"
    ],
```

-   добавить поле `params`, внутри которого задать конфиг:

```
    "params": [
        "{\"extendConfig\":{\"banner\":{\"blockIds\":{\"home\":\"R-I-XXXYYY-ZZZ\"}}}}"
    ]
```

### Пример того, как можно переписать уже существующее поле в конфиге:

```
    "params": [
        "{\"extendConfig\":{\"banner\":{\"blockIds\":{\"home\":\"R-I-XXXYYY-ZZZ\"}}}}"
    ]
```

### А вот так можно добавлять новое:

```
    "params": [
        "{\"extendConfig\":{\"banner\":{\"blockIds\":{\"newField\":\"R-I-XXXYYY-ZZZ\"}}}}"
    ]
```

### Так же можно комбинировать обновление и добавление новых полей:

```
    "params": [
        "{\"extendConfig\":{\"banner\":{\"blockIds\":{\"newField\":\"R-I-XXXYYY-ZZZ\",\"home\":\"R-I-XXXYYY-GGG\"}}}}"
    ]
```

### В конфиг можно скалдывать более сложные структуры вместо строки с ключом, например

```
    "params": [
        "{\"extendConfig\":{\"banner\":{\"blockIds\":{\"newField\":{\"hd\":\"R-I-XXXYYY-ZZZ\",\"sd\":\"R-I-XXXYYY-GGG\"}}}}}"
    ]
```

В этом примере, для нового поля `newField` мы завели новый объект, включающий себя два поля `hd` и `sd`:

```
    {
        "hd": "R-I-XXXYYY-ZZZ",
        "sd": "R-I-XXXYYY-GGG"
    }
```
