# Инструмент для конфигурирования моделей

### delete-model
Удалить модель из таблицы

- `--partner-id`
- `--score-name`

Пример
```
./config delete-model --partner-id internal --score-name internal-score-1234
```

### turn-off
Отключить регулярный пересчет модели

- `partner-id`

Пример
```
./config turn-off --partner-id internal --score-name internal-score-1234
```


### turn-on
Включить регулярный пересчет модели

- `partner-id`

Пример
```
./config turn-on --partner-id internal --score-name internal-score-1234
```
