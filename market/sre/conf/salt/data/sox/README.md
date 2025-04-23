Документация: https://wiki.yandex-team.ru/market/administration/marketsoxkeeper/
# Добавление секрета

    # Создание нового файла
    bin/soxkeeper_new_file groups/<group>/<file>
    # Редактирование существующего файла
    bin/soxkeeper_edit_file groups/<group>/<file>

    arc add <modified files>
    arc commit -m 'CSADMIN-XXX commit message'
    arc pr create --push

## С мастера

    # Накатить секреты на хост
    sudo salt gravicapa03v.market.yandex.net ...

    # На кондукторную группу
    sudo salt -N mi_orn-testing ...

Host: salt01e.market.yandex.net, salt01h.market.yandex.net

    sudo salt gravicapa03v.market.yandex.net state.sls formulaes.soxkeeper.datasources
    sudo salt gravicapa03v.market.yandex.net state.apply #накатить всё

## С хоста

На хосте новый salt, если на нём установлен deb-пакет yandex-market-salt-s2-minion-conf или если
в конфигах в `/etc/salt` указаны мастера `salt01e.market.yandex.net, salt01h.market.yandex.net`.

    sudo salt-call state.sls formulaes.soxkeeper.datasources
    sudo salt-call state.apply #накатить всё

