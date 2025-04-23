# getter

1. [wiki](https://wiki.yandex-team.ru/market/development/getter/)
2. [Облачный data-getter](https://wiki.yandex-team.ru/market/sre/clouddata-getter/)
3. [conductor](http://c.yandex-team.ru/packages/yandex-market-data-getter)

## development
Как собрать getter и все используемые им программы:
```
make
```
Как собрать только геттер и запустить его:
```
./run
```
Список всех сервисов:
```
./run ls
```
Получить файл с курсами валют:
```
./run get currency_rates
ls tmp/currency_rates/recent/currency_rates.xml
```
## Warnings
* При переименовании или перемещении файлов старые файлы удаляются после релиза getter-а.
Так как релизы getter-а и потребителей (например, guruindexer) не совпадают, нужно
создавать симлинки, чтобы избежать ошибок отсутствия файлов.
