# FirstParty Services

* [Очередь](https://st.yandex-team.ru/FPS) разработки
* [Очередь](https://st.yandex-team.ru/OPPB) проектных тикетов

## Разработчику

1. Размещаем на компьютере токен для доступа к YT. [Получить](https://oauth.yt.yandex.net) токен.
1. Монтирование репозитория.

   [Документация](https://arc-vcs.yandex-team.ru/docs) по arc

    - Получить oauth-токен по ссылке - https://nda.ya.ru/t/qPiF_BwS3WKLuC, и положить его в `~/.arc/token` . Правильно выставить права
      на токен под Linux
        ```bash
        ARC_TOKEN='xxx'
        mkdir -p ~/.arc ; chmod 700 ~/.arc ; echo -n $ARC_TOKEN > ~/.arc/token ; chmod 400 ~/.arc/token
        ```
    - В зависимости от операционной системы:
        - Linux - установить пакет fuse `sudo apt install fuse`;
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

2. Добавляем `ya` из Аркадии в PATH
 ```bash
 ln -s ~/arcadia/ya ~/bin/ya
 ```
1. Настраиваем дополнительные утилиты для работы
    ```bash
    ln -s ~/arcadia/market/fps/bin/idea.sh ~/bin/idea-project
    ln -s ~/arcadia/market/lilucrm/bin/idea-local.sh ~/bin/idea-local
    ```
4. Добавьте себя в аркадийную группу [market-fps](https://a.yandex-team.ru/arc/trunk/arcadia/groups/market-fps)
5. Добавляем telegram-бота *[YaNotifyBot](https://h.yandex-team.ru/?https%3A%2F%2Ft.me%2Fyanotifybot%2F)*, который
используются для оповещений об пулл-ревестах.


