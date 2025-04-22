## Запуск на дев стенде

1. Собираем архив
```shell
ya package package.json --target-platform=linux
```
2. Отправляем на дев сервер с помощью scp
```shell
scp formalizer.9019786.tar.gz user@braavos.market.yandex.net:/home/user/dev
```
3. Разархивируем:
```shell
tar -xvzf formalizer.9019786.tar.gz
```
4. Переходим в директорию formalizer.
5. Создаем директорию для выгрузок, например data
6. Переходим в директорию для выгрузок
7. Скачиваем выгрузку (подставь нужную ссылку)
```shell
sky get -pwu rbtorrent:8bbfe0e7331bd57a77311eb5a9a9d849bbf9cccb
```
8. Прописываем нужные пути в проперти 01_default-formalizer.properties
9. Проверяем, что для юзера задана переменная JAVA_HOME. Задать, если нет (путь для примера)
```shell
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```
10. Запустить из корня formalizer
```shell
./bin/formalizer-start.sh
```
11. Могут возникнуть невнятные ошибки с адресами - скорее всего заняты порты.
Убедись, что нет твоего уже запущенного инстанса.
Если запущены чужие, смени порты: http.port и debug.port в проперти файлах
