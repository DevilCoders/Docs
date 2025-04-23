## Инструменты для дебага на embedded устройствах

Все программы собраны полностью статически с MUSL libc, что делает их
независимыми от остального юзерспейса.

### Состав

* gdb
* gdbserver
* strace
* tcpdump
* dropbear ssh

### Поддерживаемые платформы

* aarch64-musl: 64-битные ARM платформы (Станция, Модуль, Dexp)
* armv7a-musleabihf: 32-битные ARM платформы (все остальные)

### Как получить

Запустить `ya make` в поддиректории нужной платформы. Программы будут скачаны из
Sandbox.

### Как пересобрать

Правила сборки основаны на системе сборки NixOS и лежат в поддиректории `build/`. 
До начала работы нужно инициализировать окружение сборки Nix (так, чтобы была доступна утилита `nix`).

Сборка всех утилит запускается скриптом `build.sh`. Цели сборки описаны в файле
`build/yandexio.nix`.

### gdbserver + gdb

1) запушить gdbserver на девайс `adb push gdbserver /`
2) прокинуть порты `adb forward tcp:1234 tcp:1243`
3) запустить gdbserver на колонке 
```
adb shell
chmod 777 gdbserver
export LD_LIBRARY_PATH=/system/vendor/quasar/libs
./gdbserver localhost:1234 /system/vendor/quasar/maind --yandexmini
```
4) зайти в папку `debug` сброки
```
ya tool gdb --args maind --yandexmini
target remote localhost:1234
continue
```
