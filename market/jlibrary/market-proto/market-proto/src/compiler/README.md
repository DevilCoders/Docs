#Как собрать прото компилятор

Для сборки компилятора необходимо для начала создать protoc компилятор
Для этого:
- Исходники версии 2.5.0 положить в папку market-proto/market-proto/src/compiler/protobuf-2.5.0
- Далее собрать protobuf по инструкции тут: https://github.com/google/protobuf/blob/master/src/README.md

**ВНИМАНИЕ!** под linux и под mac os я собирал с некоторыми особенностями:
1) `$ ./configure --disable-shared` # конфигурировал с флагом --disable-shared
2) `$ sudo ldconfig # refresh shared library cache.` - НЕ выполнял этот шаг
3) под mac os я устанавливал пакеты вместо 
`$ sudo apt-get install autoconf automake libtool curl make g++ unzip`
использовал
`$ brew install autoconf`, `$ brew install automake` и т.д.

***nix:**
1) Собираем protobuf. Если из коробки протобуф не собирается, обновите  libtool до версии 1.5.24
2) Запускаем `./compile.sh`

**windows:**
1) Устанавливаем mingw с поддержкой g++, msys
2) Собираем protobuf, либо копируем либы bin/libs/* в /mingw/lib
3) Запускаем `./compile.sh`

P.S. Машины на каких происходила сборка
- linux - дев сервер (braavos)
- mac os - моя девелоперская тачка
