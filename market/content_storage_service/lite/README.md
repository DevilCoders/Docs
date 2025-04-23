# Интеграционные (lite) тесты content-storage

Наши тесты написаны на 3 питоне. Чтобы все завелось нужно собрать себе свежий аркадийный питон:
```bash
ya ide venv --venv-root=<путь, где будет лежать собранный питон>
```
Для удобства можно добавить алиас, например:
```bash
alias py-arc3=/home/d-burkov/venv-cs/bin/python3
```

Теперь можно спокойно запускать тесты, в том числе и под дебагом:
```bash
py-arc3 lite/mt/test_fast_cards.py -- запустить весь набор тестов

py-arc3 lite/mt/test_card_info.py -t test_model_all_fields -- запустить конкретный тест из набора

py-arc3 lite/mt/test_card_info.py -t test_model_all_fields -d -- запус теста под gdb
```