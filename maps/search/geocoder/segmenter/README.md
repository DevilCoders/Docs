# Сегментатор адресного запроса
[[toc]]

## Устройство сегментатора
[устройство сегментатора на вики](https://wiki.yandex-team.ru/vladimirzajjcev/cheats/services/geocoder/segmenter/)

## Отладка
Для отладки предлагается использовать консольную утилиту: tools/segtest
Она распечатывает разбор запроса, читаемого из консоли, примененные правила и т.п.

## Запуск консольного отладчика
```bash
ya make -r data
ya make -r tools/segtest
./tools/segtest/segtest data
```
