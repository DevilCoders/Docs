#i-local-file-uploader#

##Описание##
Блок для загрузки файла из файловой системы.
Предоставляет метод openFileDialog для открытия окна загрузки файла из файловой системы.
Генерирует событие select при выборе в этом окне файла для загрузки.

В общем виде работа с блоком осуществляется следующим образом:

1. С помощью BEM.create(name, params) создаем инстанс блока нужной модификации.
2. В момент создания вторым параметром передаем базовые параметры инстанса.
3. Используем полученный инстанс.

##Параметры BEM.create##
mimeTypes {Array} - mime-типы файлов валидных для загрузки. При указании данного параметра в диалоговом окне файлы
с типами отличными от указанных будут недоступны для выбора (это возможность не поддерживается в
большинстве мобильных браузеров введено как дополнительное украшательство)
name - имя поля файла

###Автор###
[evolkowa](https://staff.yandex-team.ru/evolkowa)
