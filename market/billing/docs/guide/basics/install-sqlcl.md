# Установить SQLcl (sqlcl)

## Что такое, зачем, почему { #theory }

sqlcl &mdash; новый и относительно удобный консольный клиент к оракловым БД (удобнее, чем sqlplus)

С сайта Oracle:
```
It allows you to interactively or batch execute SQL and PL/SQL.
SQLcl provides in-line editing, statement completion, and command recall for a feature-rich experience,
all while also supporting your previously written SQL*Plus scripts. 
```

## Установка (MacOS, Linux) { #install }


1. Идем на сайт вендора: <https://www.oracle.com/database/technologies/appdev/sqlcl.html>
2. Нажимаем кнопку `Download`, оказываемся на странице <https://www.oracle.com/tools/downloads/sqlcl-downloads.html> (можно и сразу переходить сюда)
3. В табличке есть ссылка на скачивание ровно одного файла с названием вида `sqlcl-21.2.2.223.0914.zip` &mdash; скачиваем файл
4. Распаковываем архив. Из командной строки: `unzip sqlcl-(...).zip`
5. Получили каталог `sqlcl` &mdash; там все программы и библиотеки
6. Чтобы клиент стыковался с нашей тулзой `mb-sql`, даем исполняемому файлу новое имя: `cp sqlcl/bin/sql sqlcl/bin/sqlcl`
7. Каталог `sqlcl` помещаем в подходящее место. Если не можешь определиться &mdash; клади в домашний каталог: `mv sqlcl ~`
8. Записываем каталог в `$PATH`: в `~/.bashrc` или `~/.bash_profile` или `~/.zprofile` добавляем:
    ```
    export PATH=$PATH:<путь до каталога sqlcl>/bin
9. В уже открытом терминале перепременить файл из предыдущего пункта:
    ```
    source (подставить свой файл: ~/.bashrc|~/.bash_profile|~/.zprofile)
    ```

**Проверить успех:** `sqlcl -v`  
В норме выглядит примерно так:
```
$ sqlcl -v

SQLcl: Release 21.2.2.0 Production Build: 21.2.2.223.0914
```


## Ссылки { #links }

* Сайт Oracle: <https://www.oracle.com/database/technologies/appdev/sqlcl.html>
* Страница скачивания <https://www.oracle.com/tools/downloads/sqlcl-downloads.html>
* Сторонняя инструкция по установке sqlcl: <https://oracle-base.com/articles/misc/sqlcl-installation>
* Обсуждение ограничений sqlplus и преимуществ sqlcl:
  * <https://stackoverflow.com/a/15474083/2731799>
  * <https://blog.dbi-services.com/automatic-column-formatting-in-oracle-sqlplus/>

