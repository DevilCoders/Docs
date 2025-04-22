Наверно, когда-нибудь можно будет переписать это под `ya make`.
Сам бот крутится на ВМ [mobnavi-qa-slack](https://qyp.yandex-team.ru/?sort=abc&order=asc&my=no&name=mobnavi-qa-slack).

# Папки и файлы
```
$ tree
.
├── readme.md
├── src                 # исходники бота
│   ├── exp_to_url.py       # генератор интентов и QR-кодов по номеру выборки эксперимента
│   ├── slack_bot.py        # main-скрипт бота
│   └── sup_push.py         # отправлялка тестовых пушей МЯК через SUP
└── tools               # вспомогательные инструменты
    ├── initial_setup.sh    # первоначальная настройка необходимого для работы бота окружения
    └── start.sh            # скрипт для запуска бота в условиях VM в QYP
```


# Установка
Предварительно нужно настроить ssh на своей локальной машине: [wiki](https://wiki.yandex-team.ru/security/ssh/)

Включаем локально проброс ssh-agent.
Для этого:
 
    sudo nano /etc/ssh/ssh_config
и удаляем строку "ForwardAgent no", если такая есть.

В `$HOME/.ssh/config` добавляем секцию:

    Host mobnavi-qa-slack.sas.yp-c.yandex.net
       ForwardAgent yes
Где mobnavi-qa-slack.sas.yp-c.yandex.net – адрес ВМ в QYP, на которой крутится бот.

Добавляем свой ключ (на примере `$HOME/.ssh/id_rsa`) в ssh-agent:

    ssh-add $HOME/.ssh/id_rsa

После чего подключаемся к вм по ssh.
На удалённой машине:

    # выкачиваем код впервые
    svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/mobile/geo/qa/navi/catbug_slack_app $HOME/slack-app

    # Запускаем скрипт, устанавливающий всё необходимое
    cd $HOME && 
    cp slack-app/tools/initial_setup.sh ./ && 
    bash initial_setup.sh && 
    rm initial_setup.sh


# Запуск бота
Следует выполнять при первом запуске или после внесения изменений в код.
Или если бот сломался.

Запустить на удалённой машине:

    cd $HOME && 
    cp slack-app/tools/start.sh ./ && 
    bash start.sh && 
    rm start.sh
Либо на локальной:

    ssh mobnavi-qa-slack.sas.yp-c.yandex.net '
            bash --login -c "
                cd $HOME && 
                cp slack-app/tools/start.sh ./ && 
                bash start.sh && 
                rm start.sh
        "
    '

Где mobnavi-qa-slack.sas.yp-c.yandex.net – адрес машины, на которой крутится бот.

# Тестирование и отладка локально
Для тестирования можно создать своё приложение в слаке в отдельном воркспейсе и играться с ним, храня его секреты в соответствующих переменных окружения.
Используемые переменные можно подсмотреть в ```catbug_slack_app/tools/start.sh```
