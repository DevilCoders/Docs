# Структура пакета

Основой для формирования пакета является каталог определенной структуры, в котором размещен набор файлов с регламентированными именами и заданным форматом их содержимого. Шаблоны всех файлов, необходимых для сборки пакета, могут быть сгенерированы с помощью программы `dh_make`.

{% include [Building-buildingnote](./_includes/concepts/Building/id-Building/buildingnote.md) %}


Пример содержимого каталога, сгенерированного :
```no-highlight
|-- mypackage
|   `-- debian
|       |-- README
|       |-- README.Debian
|       |-- changelog
|       |-- compat
|       |-- control
|       |-- copyright
|       |-- cron.d.ex
|       |-- dirs
|       |-- docs
|       |-- emacsen-install.ex
|       |-- emacsen-remove.ex
|       |-- emacsen-startup.ex
|       |-- init.d.ex
|       |-- init.d.lsb.ex
|       |-- manpage.1.ex
|       |-- manpage.sgml.ex
|       |-- manpage.xml.ex
|       |-- menu.ex
|       |-- mypackage.default.ex
|       |-- mypackage.doc-base.EX
|       |-- postinst.ex
|       |-- postrm.ex
|       |-- preinst.ex
|       |-- prerm.ex
|       |-- rules
|       `-- watch.ex
```

Файлы, использующиеся при сборке и дальнейшей обработке пакета, находятся в каталоге `debian`. Расширение `ex` указывает на то, что данный шаблон может не использоваться при сборке простых пакетов. Чтобы использовать такой шаблон, необходимо удалить из имени файла расширение `ex` и внести изменения в его содержимое.

Содержимое каталога `debian` можно разделить на следующие категории:
- **Основные управляющие файлы**. Данные файлы обязательны для корректной сборки пакета. Такими файлами являются `control`, `rules `и `changelog`.
- **Скрипты сопровождения**. Набор скриптов, выполняемых перед установкой/удалением пакета, и после его установки/удаления: `preinst`, `prerm`, `postinst`, `postrm`.
- **Скрипты, выполняемые в процессе загрузки и останова системы**. Корректная работа программ, включенных в пакет или связанных с ним, может требовать выполнения определенных действий во время загрузки и останова операционной системы. В Linux-системах последовательность таких действий обычно определяется скриптами, находящимися в каталоге `/etc/init.d`. Для формирования таких скриптов предназначены файлы `init.d`, `init.d.lsb`.
- **Скрипты, выполняемые по расписанию**. Корректная работа программ, включенных в пакет или связанных с ним, может требовать выполнения определенных действий, выполняемых по расписанию. За выполнение таких действий в Linux-системах обычно отвечает программа `cron`. За внесение изменений в расписание `cron`, отвечает файл `cron.d`.
- **Создание дополнительных каталогов**. Часть каталогов, необходимых для работы программ пакета или связанных с ним, создается автоматически во время установки пакета (т. е. во время выполнения команды `make install`). Если установочные инструкции make не предполагают создания некоторых каталогов, для создания таких каталогов можно использовать файл `dirs`.
- **Документация на пакет**. В состав пакета часто включают сопутствующую информацию: документацию, справочные страницы man, README-файлы, информацию об авторских правах. Для упрощения распространения такой информации используются следующие файлы: `README`, `README.Debian`, `copyright`, `manpage.1`, `manpage.sgml`, `manpage.xml`, `docs`, `<mypackage>.doc-base`.
- **Меню для программ пакета**. Диспетчеры окон обычно поддерживают меню программ. Для включения в меню оконного менеджера пунктов, связанных с программами пакета, используется файл `menu`.
- **Обновление пакета**. Распространенным методом отслеживания изменений в пакетах является использования программ `uscan` и `uupdate`. Файл `watch` содержит информацию, необходимую данным программам для отслеживания изменений в пакете.
- Особенности пакета для _Emacs_. Если пакет содержит расширения редактора _Emacs_, то их обработка конфигурируется с помощью файлов `emacsen-install`, `emacsen-remove` и `emacsen-startup`.
- **Совместимость пакета с различными версиями debhelper**. Если для обработки пакета используется набор программ, включенный в пакет `debhelper` (как, например, в примерах, описанных в данном документе), то может возникнуть проблема совместимости. Так следующая версия `debhelper` может требовать для корректной работы работы иной структуры каталога пакета, включенных в него файлов или их содержимого. Для указания версии debhelper, которая корректно работает с данным пакетом, используется файл `compat`.

# Файлы каталога debian
Файл | Описание
----- | -----
**Основные управляющие файлы**
[control](http://www.debian.org/doc/manuals/maint-guide/dreq.en.html#control) | Информация, используемая `dpkg`, `dselect` и другими программами для работы с пакетами.
[rules](http://www.debian.org/doc/manuals/maint-guide/dreq.en.html#rules) | Набор правил make, используемых программой `dpkg-buildpackage` при сборке пакета и сопутствующих действиях.
[changelog](http://www.debian.org/doc/manuals/maint-guide/dreq.en.html#changelog) | Данные, используемые программой `dpkg` и другими для получения информации о параметрах пакета (версии, критичности применения и т. д.).
**Скрипты сопровождения**
[preinst](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#maintscripts) | Shell-скрипт, выполняемый перед установкой пакета.
[postinst](http://www.debian.org/doc/maint-guide/ch-dother.ru.html#maintscripts) | Shell-скрипт, выполняемый после установки пакета.
[prerm](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#maintscripts) | Shell-скрипт, выполняемый перед удалением пакета.
[postrm](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#maintscripts) | Shell-скрипт, выполняемый после удаления пакета.
**Скрипты, выполняемые в процессе загрузки и останова системы**
[init.d](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#initd) | Shell-скрипт для генерирования скриптов, выполняемых во время загрузки и останова системы.
[init.d.lsb](http://www.debian.org/doc/maint-guide/ch-dother.en.html#initd) | Shell-скрипт для генерирования скриптов, выполняемых во время загрузки и останова системы. Используется при подготовки пакета для Linux-систем, удовлетворяющих стандарту [LSB](http://ru.wikipedia.org/wiki/Linux_Standard_Base).
**Скрипты, выполняемые по расписанию**
[cron.d](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#crond) | Набор записей, включаемый в расписание `cron`.
**Создание дополнительных каталогов**
[dirs](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#dirs) | Список каталогов, которые должны быть созданы во время установки пакета.
**Документация на пакет**
README | Любая информация о пакете, выраженная в произвольной форме.
[README.Debain](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#readme) | Любая информация, относящаяся к пакету и отличия между исходной программой и программой, включенной в пакет (если таковые имеются).
[copyright](http://www.debian.org/doc/manuals/maint-guide/dreq.en.html#copyright) | Информация о местнонахождении исходной программы и авторских правах и лицензионное соглашение.
[manpage.1](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#manpage1) | Стандартная справочная страница man (в формате nroff), описывающая пакет.
[manpage.sgml](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#manpagesgml) | Справочная страница man, описывающая пакет, в формате DocBook SGML.
[manpage.xml](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#manpage) | Справочная страница man, описывающая пакет, в формате DocBook XML.
[docs](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#docs) | Список документов, которые должны быть размещены в стандартном каталоге документации на пакет (обычно это `/usr/share/doc/<mypackage>`).
[<mypackage>.docbase](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#doc-base) | Информация о формате и местоположении дополнительной документации на пакет.
**Меню для программ пакета**
[menu](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#menu) | Описание пункта меню оконного менеджера, связанного с содержимым пакета.
**Обновление пакета**
[watch](http://www.debian.org/doc/manuals/maint-guide/dother.ru.html#watch) | Конфигурационный файл для программ `uscan` и `uupdate`, содержащий информацию о расположении источников обновлений пакета.
**Особенности пакета для Emacs**
[emacsen-install](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#emacsen) | Shell-скрипт установки расширения для `Emacs`.
[emacsen-remove](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#emacsen) | Shell-скрипт удаления расширения для `Emacs`.
[emacsen-startup](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#emacsen) | Код на языке LISP, который должен выполняться при загрузке `Emacs`.
**Совместимость пакета с различными версиями debhelper**
[compat](http://www.debian.org/doc/manuals/maint-guide/dother.en.html#compat) | Версия `debhelper`, с которой данный пакет заведомо совместим.

{% note info %}

Просмотреть содержимое готового deb-пакета можно с помощью команды:

```
dpkg -c <имя-пакета>.deb
```

{% endnote %}

- [Создание пакетов в Верстке](http://wiki.yandex-team.ru/verstka/static#sozdaniesobstvennogopaketa)
