# Образ контейнера со всем необходимым чтобы запустились юнит-тесты для balance-paysys
*почти полная копия toolsbase*

Сборка:
```
docker build . -t paysys-base
```

Готовый образ можно стянуть тут: registry.yandex.net/balance/paysys-base

# Использование контейнера
В контейнере не предусмотрено никакой входной точки, потому как запуск тестов дело индивидуальное. 
Для примера можно запустить вот так: 
```bash
docker run -ti --rm --name paysys-base \
    -v ~/paysys:/paysys \
    -v ~/tools:/tools \
    -v ~/utils:/utils \
    -v ~/logs:/var/log/yb \
    registry.yandex.net/balance/paysys-base ./runner.sh
``` 
Это запустит все тесты из папки `balance-paysys/tests` при условии что всё правильно у вас настроено. 
Захардкоржен tns-алиас balance.yandex.ru, возможно стоит перейти на TEST_BALANCE_YANDEX_RU.
