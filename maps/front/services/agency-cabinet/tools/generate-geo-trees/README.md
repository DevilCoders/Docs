## Генератор дерева геообъектов

Стороит по geobase https://geoadmin.yandex-team.ru/ дерево мест

### Как запустить

1. Поместить файл geodata6.bin в \_\_dirname/resources/

Скачать файл geodata6.bin из sandbox ресурсов

https://sandbox.yandex-team.ru/resources?type=GEODATA6BIN_STABLE&limit=20&created=14_days

или

https://sandbox.yandex-team.ru/resources?type=GEODATA6BIN_TESTING&limit=20&created=14_days

2. Скачать файл borders.tar.bz2 https://proxy.sandbox.yandex-team.ru/1366982726/borders.tar.bz2
3. Разархивировать borders.tar.bz2 в \_\_dirname/resources/borders
4. Запустить скрипт из корня

```
npm run generate-geo-trees
```
