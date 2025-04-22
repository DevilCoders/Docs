---
title: Настройка окружения для разработки
---

# Настройка окружения для разработки

### Настраиваем arc ###
1. Устанавливаем `arc` и скачиваем репозиторий по [инструкции](https://wiki.yandex-team.ru/arcadia/Arcadia-Starter-Guide/#kakskachatrepozitorijj)

    {% note tip %}

    Рекомендую сохранить путь до аркадии в переменную `$ARCADIA_ROOT` в `~/.bashrc`. Переменная пригодится в дальнейшем.

    {% endnote %}

2. Настраиваем отображение текущей ветки по [инструкции](https://wiki.yandex-team.ru/arcadia/Arcadia-Starter-Guide/#jaxochuvsegdavidettekushhujuvetkuvterminale)
3. Настраиваем таб-дополнение arc по [инструкции](https://doc.yandex-team.ru/arc/setup/arc/hacks.html)

    {% note info %}

    [Инструкция](https://wiki.yandex-team.ru/arcadia/Arcadia-Starter-Guide/#kakzakommititkodvobshhijjrepozitorijj) "Как закоммитить в общий репозиторий"

    {% endnote %}

### Настраиваем утилиту ya ###
1. Сохраняем токен
    ```
    ya whoami --save-token
    ```
1. Настраиваем автодополнение по [инструкции](https://docs.yandex-team.ru/yatool/commands/completion)

### Настраиваем переменные окружения ###
- YP OAuth-Token [получаем](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7) и выполняем:
    ```
    cd ~ && mkdir .yp
    echo <OAuth-Token> > .yp/token
    ```

- YQL OAuth-Token [получаем](https://yql.yandex-team.ru/?settings_mode=token) и сохраняем
    ```
    cd ~ && mkdir .yql
    echo <OAuth-Token> > .yql/token
    ```

- YT OAuth-Token [получаем](https://oauth.yt.yandex.net/) и сохраняем
    ```
    cd ~ && mkdir .yt
    echo <OAuth-Token> > .yt/token
    ```

### Настраиваем IDE ###
1. Устанавливаем IDE

    {% list tabs %}

    - Java

      [Idea Ultimate](https://www.jetbrains.com/idea/download)
      

    - Python

      [PyCharm](https://www.jetbrains.com/pycharm/download/)

    - Go

      [GoLang](https://www.jetbrains.com/go/download/)

    {% endlist %}

2. Устанавливаем  и настраиваем плагины:

    {% list tabs %}

    - IntelejiIdea

      - `lombok` ([инструкция](https://wiki.yandex-team.ru/disk/java/faq/#nastraivaemideadljarabotyslombok))
      - `arcadia plugin` ([инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/#как-установить-плагин))

    - PyCharm

      - `arcadia plugin` ([инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/#как-установить-плагин))

    - Go

      - `arcadia plugin` ([инструкция](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/#как-установить-плагин))

    {% endlist %}

3. Гененируем Idea проект из исходников
   ```
   cd $ARCADIA_ROOT
   ya ide idea -k -r $IDEA_PROJECT_ROOT -l api --group-modules=tree
   ```
   По завершению на консоль выведется
   ```
   ...
   Ok
   Info: Successfully generated idea project: /home/$USER/prog/idea/travel_api
   Info: Devtools IntelliJ plugin (Latest stable IDEA is required): https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij/README.md
   Info: Codestyle config: /home/$USER/.ya/tools/v4/441758406/intellij-codestyle.jar. You can import this file with "File -> Manage IDE Settings -> Import settings..." command. After this choose "yandex-arcadia" in code style settings (Preferences -> Editor -> Code Style).
   ```

   {% note info %}

   При изменении зависимостей проекта необходимо перезапускать команду.
   Через -l можно добавлять/удалять модули в проекте как исходники.

   {% endnote %}

1. Выполняем настройку code style по описанию из блока **INFO: Codestyle config** в выводе предыдущего пункта

