yandex-kernel-params
====================

Helper для удобного добавления/удаления параметров ядра

Общее описание и принцип работы
-------------------------------

Posix shell-скрипт zz-yandex-kernel-params.cfg живет в каталоге /etc/default/grub.d и
вызывается каждый раз, при вызове update-grub, или grub-mkconfig -o /boot/grub/grub.cfg.
Во время выполнения, скрипт ищет в каталогах /etc/yandex/kernel-parameters/present и
/etc/yandex/kernel-parameters/absent *.cfg-файлы, в которых перечислены параметры ядра,
которые должны быть добавлены (present каталог), или должны отсутствовать в (absent каталог).
Параметры перечисляются по одному в каждой строке файлов.
Исходя из этих записей, содержимого файла /etc/default/grub и иных *.cfg-файлов в каталоге
/etc/default/grub.d, скрипт формирует строку с параметрами ядра и сохраняет её в переменной
GRUB_CMDLINE_LINUX_DEFAULT. Данную переменную использует grub-mkconfig для формирования
/boot/grub/grub.cfg.

Ссылки
------

[sandbox job to build debian package](https://sandbox.yandex-team.ru/task/107448251/view)
