# Диски и файловые хранилища

Для работы с данными к [виртуальным машинам](vm.md) можно подключать следующие ресурсы {{ compute-name }}:

| Ресурс | Описание |
| ----- | ----- |
| [Диск](disk.md) | Виртуальный аналог физического накопителя, подключаемый к ВМ как [сетевое блочное устройство](https://en.wikipedia.org/wiki/Network_block_device). Один диск может быть подключен только к одной ВМ. С файловой системы диска можно снять копию — [_снимок диска_](snapshot.md). |
| [Файловое хранилище](filesystem.md) | _Файловые хранилища находятся на стадии [Preview](../../overview/concepts/launch-stages.md)._ <br> Виртуальная файловая система, подключаемая к ВМ через интерфейс [Filesystem in Userspace]{% if lang == "en" %}(https://en.wikipedia.org/wiki/Filesystem_in_Userspace){% else %}(https://ru.wikipedia.org/wiki/FUSE_(модуль_ядра)){% endif %} (FUSE) как устройство [virtiofs](https://www.kernel.org/doc/html/latest/filesystems/virtiofs.html). Одно файловое хранилище может быть подключено к нескольким ВМ одновременно. |

К каждой ВМ можно подключить несколько дисков (помимо обязательного загрузочного) и несколько файловых хранилищ.

Для дисков и файловых хранилищ действуют технические ограничения на [операции чтения и записи](storage-read-write.md).