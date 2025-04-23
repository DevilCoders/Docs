# Сборщики

Проект IMAP/POP3 сборщиков

# Сборка

1. ```git clone git@github.yandex-team.ru:yplatform/yservice_rpop.git && cd yservice_rpop``` клонируем репозиторий.
2. ```git submodule update --recursive --init``` рекурсивно клонируем все подмодули
3. ```(mkdir build; cd build; cmake -DCMAKE_BUILD_TYPE=Debug ..)``` создаем папку ```build``` и переходим в нее. Там создаем сборочное дерево ```cmake```.
4. ```make -j`nproc` ``` собираем всё вместе.
5. ```make test``` запускаем все тесты.

# Конфигруация

Данный проект использует генерацию конфигов на этапе сборки cmake.
Для этого используется скрипт - etc/conf_generator/conf_generator.py

# conf_generator.py
Принимает 3 аргумента:
* *setup* - в каком сетапе настраиваем проект - yarm, yrpop, в будущем - collectors и dev, в основном определяет какие модули будут включены в конфиг, а так же пути лог файлов.
* *env* - окружение для запуска - qa, loadtest, production, (в будущем - dev) от него в основном зависит в какие хосты будут ходить сборщики
* *ouput_file* - выходной файл для записи конфига.

## Пример использования:
```
./conf_generator.py yrpop qa yrpop-qa.xml
```
