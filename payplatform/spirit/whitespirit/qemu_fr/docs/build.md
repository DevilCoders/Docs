Пакеты, необходимые для сборки
 - devscripts
 - build-essential
 - git libglib2.0-dev libfdt-dev libpixman-1-dev zlib1g-dev flex bison ninja-build ruby
 <!--- gcc-arm-linux-gnueabihf binutils-arm-linux-gnueabihf-->

Прочитать про подпись и закгрузку пакетов в [dist](https://doc.yandex-team.ru/Debian/deb-pckg-guide/concepts/About.html)

Установить [fpm](https://fpm.readthedocs.io/en/latest/installing.html)
 - `gem install --no-ri --no-rdoc fpm`
 
 Поправить шаблон для создания \*.changes файла, который находится примерно здесь `/var/lib/gems/2.5.0/gems/fpm-1.10.2/templates/deb/deb.changes.erb`:
 - добавить надо `Changed-By: <%= maintainer %>`

Запустить сборку
 - `./fpm_build.sh "1.0.6" 'Kirill Isupov (yandex-deb-sign) <isupov@yandex-team.ru>'`

Информация
 - [компиляция qemu](https://wiki.qemu.org/Hosts/Linux)
 - [glibc для ARMhf](https://packages.debian.org/ru/stretch/armhf/libc6/download)
 - Можно использовать пакет libc6-armhf-cross (скрипт скачивает и запаковывает в пакет копию из пункта выше), библиотеки будут вот здесь /usr/arm-linux-gnueabihf
 - [про перехват функций с помощью LD_PRELOAD](https://habr.com/post/199090/)
 - К сожалению нужен патч для перехвата функции connect, патч сделан грязно, чистый путь: весь функционал перехватчика должен быть в патче
 - LD_PRELOAD в эмуляторе не перехватывает функции
