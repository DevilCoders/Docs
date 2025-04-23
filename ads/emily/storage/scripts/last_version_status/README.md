# Models validation parser tool

Тула для быстрого парсинга ошибок валидации моделей стораджа. При работе обходит инстансы валидации моделей по пути [/logos/models](https://reactor.yandex-team.ru/browse?selected=9612857), находит последний статус и выводит ошибку, если реакция упала.

## Примеры:

### Модель валидируется:

```bash
2022-06-02 17:43:54,049 | I |    libs.status_parsing:102 | get_model_info         | CPM_ssp_regular: OK
```

### Ошибка валидации:

```bash
2022-06-02 17:53:05,599 | E |    libs.status_parsing:140 | get_model_info         | VideoCompleteLClick_EShowModel_OnlyVideo_BannerID_UniqID_LLMax_90_NoCommerce_TLM: 2022-06-02 04:00:16,681 | E |          processor.lib:42  | run_validation         | Validation error: 'Metric thresholds violated: max threshold 0.63 for metrics q_auc violated: val = 0.6314856187' | state: convert
```

### Не удаётся найти реакции для парсинга:
```bash
2022-06-02 18:02:24,020 | D |    libs.status_parsing:96  | get_model_info         | CPM_F6_predict_money_from_hit_mse_9__TEST: NO REACTION INSTANCES
```


Для работы необходим [OAUTH_TOKEN](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=7184f2bfc9734a6282ad882bdf104cf1)

## Использование

```bash
# Собрать
ads/emily/storage/scripts/last_version_status$ ya make -r
```

```bash
ads/emily/storage/scripts/last_version_status$ ./last_version_status --help

  --key TEXT         Искать по ключу. Также нужно добавить опцию --model-type
  --model-type TEXT  Тип модели при поиске по ключу. mx/tsar/lm
  --lms              Все линейные модели
  --mxs              Все матрикснеты
  --tsars            Все цари
  --regular          Проверять только регулярные модели
  -h, --help         Show this message and exit.

```

