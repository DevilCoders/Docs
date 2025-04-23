# Пользовательский CRM Маркета

* [Очередь](https://st.yandex-team.ru/LILUCRM) задач
* [Очередь](https://st.yandex-team.ru/OCRM) задач операционного CRM
* Wiki [страница](https://wiki.yandex-team.ru/Market/lilucrm/) проекта
* Wiki [страница](https://wiki.yandex-team.ru/Market/Development/crm) разработчика

## Компоненты
1. *[campaign](campaign/README.md)* - маркетинговый CRM. Управление рекламной коммуникацией Маркета: рекламные email,
    push, SMS-рассылки.
2. *[triggers_platform](triggers_platform/README.md)* - триггерная платформа
3. *[operator-window](operator-window/README.md)* - OCRM (операционный CRM, окно оператора). Автоматизация колл-центра Маркета.
4. *platform_reader* - часть Платформы CRM, отвечающая за сбор информации о пользователе Маркета.
5. *[platform_api](platform_api/README.md)* - часть Платформы CRM, отвечающая за доступ к собранной информации о
    пользователе Маркета.
6. *platform_config* - конфигурация Платформы CRM. Описывает факты о пользователе, хранимые Платформой CRM.
7. *platform_core* - базовая часть Платформы CRM. Содержит общий код различных компонентов Платформы CRM.
8. *platform_sber* - компонет файлового обмена Маркета и Сбербанка.
9. *[jmf](jmf/README.md)* - набор общих компонент.

## Общая настройка проекта

1. Устанавливаем *nodejs 14.x.x* и *yarn*

    Linux:
    ```bash
    curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
    echo -e 'Package: nodejs\nPin: origin deb.nodesource.com\nPin-Priority: 1001' | sudo tee /etc/apt/preferences.d/nodejs
    sudo apt install -y nodejs
    ```
    MacOS:
    ```bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    brew install node@14
    brew link --overwrite --force node@14
    ```

1. Устанавливаем *yarn*. Дистрибутив скачиваем с официального [сайта](https://yarnpkg.com/lang/en/)

1. Размещаем на компьютере токен для доступа к YT. [Получить](https://oauth.yt.yandex.net) токен.

1. Монтирование репозитория. В Яндексе существует своя система контроля версий (VCS) - Arc. При работе с 
ним репозиторий не скачивается польностью локально, а примонтируется удаленная файловая система, 
в которой лежит весь репозиторий. Локально хранятся только изменения. 

    Документацию по Arc можно найти [тут](https://arc-vcs.yandex-team.ru/docs)

    - Получить oauth-токен по ссылке - https://nda.ya.ru/t/qPiF_BwS3WKLuC, и положить его в `~/.arc/token` . Правильно выставить права
 на токен под Linux
        ```bash
        ARC_TOKEN='xxx'
        mkdir -p ~/.arc ; chmod 700 ~/.arc ; echo -n $ARC_TOKEN > ~/.arc/token ; chmod 400 ~/.arc/token
        ```
    - В зависимости от операционной системы:
        - Linux - установить пакет fuse (`sudo apt install fuse`);
        - Mac OS - установить пакет osxfuse `brew cask install osxfuse`
    - Установить arc клиент

        - Linux (tested on Ubuntu)
            ```bash
            tmp_list=$(mktemp)
            
            cat << EOF > ${tmp_list}
            deb http://common.dist.yandex.ru/common stable/all/
            deb http://common.dist.yandex.ru/common stable/amd64/
            EOF

            sudo mv ${tmp_list} /etc/apt/sources.list.d/yandex.list

            # импортируем GPG-ключ для репозиториев выше
            sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7FCD11186050CD1A

            sudo apt update && sudo apt install yandex-archive-keyring
            
            # устанавливаем клиент
            sudo apt install yandex-arc-launcher

            # добавляем автообновление клиента
            systemctl --user enable --now arc-update.timer
            ```

        - MacOS. Для начала попробуйте установить через Self Service: https://nda.ya.ru/3VnWRL.

            Если вдруг не получится, то следуйте инструкции ниже
            ```bash
            # Установить brew tap с клиентом Arc
            brew tap --full yandex/arc https://arc-vcs.yandex-team.ru/homebrew-tap

            # Установить клиент arc
            brew install arc-launcher

            # Включение ежедневной проверки обновлений
            brew services start arc-launcher
            ```
    - Задаем переменные для дефолтных директорий arc'а и проекта. 
        В `~/.bashrc` (или любой другой файл, который читает ваш терминал при запуске) добавляем:
        + переменную `ARC_ROOT` (по умолчанию `$HOME`) в которой указываем где будет arc хранить репозиторий (будут
        созданы директории `$ARC_ROOT/arcadia`, где будет располагаться дерево файлов, и `$ARC_ROOT/arcadia_store`,
        где будут располагаться служебные файлы)
        + переменную `PROJECTS_ROOT` (по умолчанию `$HOME/projects`),
        в которой указываем, где будут генерироваться проекты для Idea
        ```bash
        export ARC_ROOT="$HOME"
        export PROJECTS_ROOT="$HOME/projects"
        ```
    - Чтобы скрипты работали без указания пути до них нужно туда же прописать добавление `~/bin` в `PATH`
        ```bash
        if [[ :$PATH: != *:"${HOME}/bin":* ]] ; then
            PATH="${HOME}/bin:${PATH}"
        fi
        ```
    - Выполняем код ниже,чтобы создать файл `~/bin/mount-arcadia`, содержащий скрипт монтирования репозитория
        ```bash
        mkdir -p ~/bin

        cat << EOF > ~/bin/mount-arcadia
        #!/usr/bin/env bash
        
        ARCADIA_FOLDER="\${ARC_ROOT}/arcadia"
        ARCADIA_STORE_FOLDER="\${ARC_ROOT}/arcadia_store"
        
        mkdir -p "\${ARCADIA_FOLDER}"
        mkdir -p "\${ARCADIA_STORE_FOLDER}"
        
        arc mount -m "\${ARCADIA_FOLDER}" -S "\${ARCADIA_STORE_FOLDER}"
        EOF

        sudo chmod +x ~/bin/mount-arcadia
        ```
    - Выполняем команду `mount-arcadia` для монтирования Аркадии. По пути `$ARC_ROOT/arcadia` появится
        примонтированный репозиторий, а по пути `$ARC_ROOT/arcadia_store` служебные файлы.
        Лучше добавить эту команду в автозагрузку, чтобы не выполнять её после каждого перезапуска ОС.

1. Добавляем `ya` из Аркадии в PATH
    ```bash
    ln -s ~/arcadia/ya ~/bin/ya
    ```

1. Настраиваем дополнительные утилиты для работы (желательно, но необязательно)
    ```bash
    ln -s ~/arcadia/market/lilucrm/bin/idea.sh ~/bin/idea-project
    ln -s ~/arcadia/market/lilucrm/bin/idea-local.sh ~/bin/idea-local
    ```

1. Подготовка проекта для Idea.
    ```bash
    ~/arcadia/market/lilucrm/bin/idea.sh
    ```
    или если выполнен пункт с дополнительными утилитами для работы
    ```bash
    idea-project
    ```
    А можно перейти в директорию любого проекта и выполнить там `idea-local $PROJECT_PATH`,
    чтобы создать Idea проект только для этого проекта, без лишних зависимостей.

1. Настройка IDEA. Установить IDEA, если этого еще не сделано.

    1. Плагин для IDEA.
        - [Установить](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij) плагин для ide с поддержкой arc-а.
        (Примечание: если возникли проблемы со ссылкой на ouath, то она действует только 1 минуту после запуска IDEA)

        - В IDEA: _File->Settings->Version Control_ добавить _VCS=Arc, Directory="${ARC_ROOT}/arcadia"_

    1. Настройка.
        * Открываем проект (_File->Open..._), расположенный по пути `~/projects/lilucrm`
        * Добавляем VCS (_File->Settings->Version Control_), выделяем */home/${user}/arcadia* и нажимаем '+' справа
        * Указываем версию java для компиляции проекта под IDEA (_File->Project Structure->SDKs_)
            * Если там нет подходящего, то найти нужный Java SDK можно скриптом
              ```shell
              TARGET_JDK_VERSION=15 # Его можно узнать либо в скрипте ./bin/idea-local.sh по параметру
                                    # -DJDK_VERSION, либо узнав какая версия JDK сейчас по умолчанию в аркадии
              # Если хотите найти просто последнюю версию JDK у вас, то оставьте TARGET_JDK_VERSION пустым
              (cd ~/.ya/tools/ && find . -type f -name javac -printf '%p ' -exec {} -version \; 2>&1 | grep "javac ${TARGET_JDK_VERSION}" | sort -V -k3 -r | head -1 | cut -d' ' -f1)
              ```
              либо командой:
              ```shell
              ya tool java17 --print-path
              ```
           * Если вы удалите `~/.ya`, то нужно будет настроить SDK по новой
        * В _File -> Settings -> Build, Execution, Deployment -> Compiler -> User-local build process VM Options_ пишем `-Djps.track.ap.dependencies=false`
        * Настраиваем стили кодирования:
            - в выводе `idea-project` была строка _Info: Codestyle config_. Далее указан путь до _intellij-codestyle.jar_
            - В IDEA идем _File->Import Settings_ `~/arcadia/devtools/intellij-codestyle/devtools-intellij-codestyle.jar`
            - Нужно снять галку `Enable EditorConfig support` (_Settings->Editor->Code Style_), чтобы было корректное форматирование

## Работа с ветками

В аркадии есть два типа веток:

1. **Пользовательские ветки** предназначены для индивидуальной разработки. Такие ветки имеют имя
   __users/${user}/branch-name__, например, _users/tesseract/LILUCRM-12345_ . Такую ветку на сервер может запушить
   только пользователь tesseract. Другие пользователи что-то делать с этой веткой на сервере не смогут.

1. **Групповые ветки** предназначены для работы над задачами сразу несколькими пользователями. Такие ветки имеют имя
   __groups/${group}/branch-name__, например, _groups/content-api/LILUCRM-12345_. Работать с такими ветками могут
   только пользователи, состоящие в аркадийной группе. Правила работы с группами содержатся в
   [инструкции](https://a.yandex-team.ru/arc/trunk/arcadia/groups/readme.md).

## Группы

Аркадийные группы используются для оповещений об пулл-ревестах в сервисы, за которые она отвечает. Ответственость
группы за сервис указывается в _ya.make_ в тэге *OWNER* (может быть указано несколько групп и конкретных сотрудников).

1. *[market-lilucrm-mcrm](https://a.yandex-team.ru/arc/trunk/arcadia/groups/market-lilucrm-mcrm)*.
    Рассылка [market-lilucrm-mcrm-commits@yandex-team.ru](https://ml.yandex-team.ru/lists/market-lilucrm-mcrm-commits/).

1. *[market-lilucrm-ocrm](https://a.yandex-team.ru/arc/trunk/arcadia/groups/market-lilucrm-ocrm)*.
    Рассылка [market-lilucrm-ocrm-commits@yandex-team.ru](https://ml.yandex-team.ru/lists/market-lilucrm-ocrm-commits/).

1. *[market-lilucrm-platform](https://a.yandex-team.ru/arc/trunk/arcadia/groups/market-lilucrm-platform)*.
    Рассылка [market-lilucrm-platform-commits@yandex-team.ru](https://ml.yandex-team.ru/lists/market-lilucrm-platform-commits/).

1. *[market-lilucrm-platform-sber](https://a.yandex-team.ru/arc/trunk/arcadia/groups/market-lilucrm-platform-sber)*.
    Рассылка [market-lilucrm-platform-sber-commits@yandex-team.ru](https://ml.yandex-team.ru/lists/market-lilucrm-platform-sber-commits/).

1. *[market-lilucrm](https://a.yandex-team.ru/arc/trunk/arcadia/groups/market-lilucrm)*.
    Рассылка [market-lilucrm-commits@yandex-team.ru](https://ml.yandex-team.ru/lists/market-lilucrm-commits/).

1. *[market-lilucrm-jmf](https://a.yandex-team.ru/arc/trunk/arcadia/groups/market-lilucrm-jmf)*.
    Рассылка [market-lilucrm-jmf-commits@yandex-team.ru](https://ml.yandex-team.ru/lists/market-lilucrm-jmf-commits/).

## Telegram

Telegram-бот *[YaNotifyBot](https://h.yandex-team.ru/?https%3A%2F%2Ft.me%2Fyanotifybot%2F)* используются для оповещений об пулл-ревестах
