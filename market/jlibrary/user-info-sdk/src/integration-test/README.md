Описание
-----
Простой тест демонстрирующий работу с `TVM`

Запуск
-----
Из bash:
 TVM_SECRET=<your_tvm_secret> ya make -tA --test-tag +ya:manual
Из idea:
 В конфигурации теста:
 1. Добавить в `VM Options`
 ```
 -Djava.net.preferIPv6Stack=true -Djava.net.preferIPv6Addresses=true
 ```
 2. Добавить в пременные окружения:
 ```
 TVM_SECRET=<your_tvm_secret>
 ```

TODO
-----
Перенести тест из запускаемых вручную, в полноценные запускаемые с секретом из sandbox
