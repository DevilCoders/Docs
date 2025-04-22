# Установить SQL*Plus (sqlplus)

{% note warning %}

Не пользуйтесь sqlplus. Пользуйтесь sqlcl, [{#T}](install-sqlcl.md).

{% endnote %}


## Что такое, зачем, почему { #theory }

sqlplus -- консольный клиент к оракловым БД

## Ubuntu

На Ubuntu 20.04 установлено по инструкции отсюда <http://jarmx.blogspot.com/2019/05/install-sqlplus-client-on-ubuntu-1804.html>

Также один раз проверено, что работает инструкция <https://www.foxinfotech.in/2019/03/how-to-install-sqlplus-in-linux-ubuntu.html>

Предположительно, можно проще:
1. <https://www.oracle.com/database/technologies/instant-client/downloads.html> &mdash; здесь пойти на страницу для Linux
2. скачать файлы `instantclient-basic-linux.x64-(версия)dbru.zip` и `instantclient-sqlplus-linux.x64-(версия)dbru.zip`. Ключевые слова в названиях: `basic` и `sqlplus`
3. Распаковать архивы из предыдущего пункта, каталог можно сделать другой:
    ```
    mkdir -p /opt/oracle
    unzip -d /opt/oracle instantclient-basic-linux.x64-...dbru.zip
    unzip -d /opt/oracle instantclient-sqlplus-linux.x64-...dbru.zip
    ```
4. Записать в `~/.bashrc` или `~/.bash_profile` или `~/.zprofile`:
    ```
    export LD_LIBRARY_PATH=/opt/oracle/instantclient_19_3:$LD_LIBRARY_PATH
    export PATH=$LD_LIBRARY_PATH:$PATH
    ```
5. В уже открытом терминале перепременить файл из предыдущего пункта:
    ```
    source (подставить свой файл: ~/.bashrc|~/.bash_profile|~/.zprofile)
    ```

**Проверить успех:** `sqlplus -V`  
В норме выглядит примерно так:
```
$ sqlplus -V

SQL*Plus: Release 21.0.0.0.0 - Production
Version 21.1.0.0.0

```

## MacOS

Предположительно, должен сработать рецепт для Ubuntu, только архивы выбирать со страницы для MacOS


## Ссылки { #links }

* <https://zwbetz.com/install-sqlplus-on-linux/>
* <https://zwbetz.com/install-sqlplus-on-a-mac/>
* <https://dba.stackexchange.com/questions/273151/how-to-install-oracles-sqlplus-on-a-mac>

