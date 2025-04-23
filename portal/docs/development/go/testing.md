# Тестирование

{% note tip %}

Морда живет под аппхостом, поэтому рекомендуется ознакомиться с полезными [cgi-параметрами для тестирования аппхоста](https://docs.yandex-team.ru/apphost/pages/cgi)

{% endnote %}

## На дев-хосте

Для тестирования нужно:
1. [Поднять на дев-хосте сервис](https://docs.yandex-team.ru/portal/development/go/#kompilyaciya), в котором сделаны изменения (например: morda-go или avocado)
2. Переопределить бэкенд в запросе, который тестируем, на свой поднятый инстанс сервиса, используя cgi-параметр:
``srcrwr=BACKEND_NAME:host:port:timeout``

### Как отследить ошибку в запросе:
Отследить путь запроса можно через [Setrace](https://setrace.yandex-team.ru/web/search). Для этого нужно взять заголовок ``X-Yandex-Req-Id`` и подставить в поисковую строку. 

### Как понять какой бэкенд нужно переопределить:
Название бэкенда вершины графа можно найти в разделе ``nodes`` в описании графа в поле ``backend_name``

[https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/MORDA](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/MORDA)
### Как определить какой граф используется при запросе:
За роутинг, отвечает ``http_adapter``, в его настройках указано соответствие пути запроса и графа.

[https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/MORDA/_routing_config.json](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/MORDA/_routing_config.json)

### Как переопределить несколько вершин/бэкендов в графе:
Можно использовать несколько парамтеров ``srcrwr=`` в одном запросе.

Но могут возникнуть проблемы при тестировании на клиентах, так как клиент может фильтровать cgi-параметры.
Можно использовать утилиту ``npx morda-dev`` для поднятия беты с переопределением нужных бэкендов.
Запускать утилиту нужно из папки дев-инстанса. 

### Как изменить таймаут вершины/бэкенда:
```
srcrwr=BACKEND_NAME:::1ms
srcrwr=VERTEX_NAME:::10s
```
Чтобы имитировать неответ вершины по таймауту, можно указать хост с закрытым портом:
```
srcrwr=VERTEX_NAME:yandex.ru:444
```

### Как переопределить Perl-бэкенд:
Для походов в Perl-бэкенд в графах Морды используются бэкенды:
* ``MORDA__MORDA_APP_BACKEND`` — основная перловая морда. Порты 18000-18009
* ``MORDA__MORDA_PERL_INIT_BACKEND`` — бэкенд ручки перла для прокидывания данных в Go-бэкенд. Порты 12000-12009

{% note info %}

Последняя цифра порта — номер инстанса, в который будет отправлен запрос. Для инстанса v199d1 порт бэкенда ``MORDA__MORDA_PERL_INIT_BACKEND`` будет 12001, для v199d2 — 12002 и так далее.

{% endnote %}

{% note info %}

Чтобы аппхост смог пойти на дев-инстанс в ручку /portal/api/search/2 (бэкенд ``MORDA__MORDA_APP_BACKEND``), нужно добавить в nginx-конфиг инстанса ``morda-v199dX/conf/templates/nginx.conf.template``  строки:
```
    ...
    location /portal/api/search/2 {
        [% PROCESS PassToBackend allow_methods => [ 'GET', 'POST'] %]
    }
}
```

{% endnote %}

### Пример
```
https://portal-hamster.yandex.ru/portal/api/search/2?srcrwr=MORDA__MORDA_PERL_INIT_BACKEND:morda-dev-v199.sas.yp-c.yandex.net:12001&srcrwr=MORDA__MORDA_GO_APP_BACKEND:morda-dev-v199.sas.yp-c.yandex.net:20223
```

В этом примере запрос попадет в граф ``morda_searchapp``.
Аппхост будет отправлять запрос к вершине ``PERL_INIT`` (бэкенд у вершины — ``MORDA__MORDA_PERL_INIT_BACKEND``) на дев-хост v199d1.
А все вершины графа, использующие бэкенд ``MORDA__MORDA_GO_APP_BACKEND``, будут обращаться к инстансу ``morda-go``, который поднят на дев-хосте v199


## На бете

После создания пулл-реквеста в аркадии будет автоматически подняты два бета-стенда — для ``avocado`` и ``morda-go``, которые будут жить, пока открыт пулл-реквест. 

![яппи-стенды в ПР](https://jing.yandex-team.ru/files/slindgre/Screenshot%20from%202021-10-28%2020-44-49.png)

По клику на кнопку, откроется Yappy с настройками стенда. Для тестирования нужен хост вида: ``mordago-pr-123456.hometest.yandex.ru``
При переводе задачи в тестирование в тикете стоит указвать именно этот хост беты, а не дев-хост.

Настоятельно рекомендуется проверять разработчику или тестировщику работоспособность поднятого хоста, сделав запрос из браузера или ПП, в зависимости от того, куда были внесены изменения.

### Как провеить на клиенте ПП:
Если есть изменения в ручке ПП, то желательно проверять их на клиенте, натравив его на бету:
  * **Android:** Дебаг-панель: URLs -> Edit custom hosts -> HOST_HOME: `mordago-pr-123456.hometest.yandex.ru/portal/api/search` (без двойки). Бету ПП с дебаг-панелью можно взять [здесь](https://teamcity.browser.yandex-team.ru/buildConfiguration/Browser_AndroidBuilds_MobileYandex_ReleaseBuilds_TestingBundle?mode=builds)
  * **iOS:** Дебаг-панель -> URL Configuration -> portal: `mordago-pr-123456.hometest.yandex.ru` (без пути). Беты для iOS [тут](https://beta.m.soft.yandex.ru/description?app=bro_search&platform_shortcut=iphoneos&branch=master-beta)

{% note info %}

Чтобы появилась возможность скачать ПП с дебаг панелью на IOS, убедитесь, что на стаффе привязан личный аккаунт Яндекса.

{% endnote %}

### Как работать с МАДМ:

Сейчас беты смотрят на продакшн-экспорты МАДМ. Если для тестирования задачи необходимы изменения в экспортах, можно привезти экспорты на бету с дев-хоста двумя способами:
1. Используя madm-agent.
   1. В pr'e зайдите в "portal: (PR) Test on beta"

   ![](https://jing.yandex-team.ru/files/cheetah/2022-03-23T14%3A18%3A23Z.113df09.png =x60){: .center} 
   
   1.2. Дождитесь зеленого состояния кубика morda-go беты и нажмите на решетку

   ![](https://jing.yandex-team.ru/files/cheetah/2022-03-23T14%3A25%3A49Z.aa97c08.png =x250){: .center} 
   

   1.3. Зайдите в артефакты и скопируйте номер pr'a

   ![](https://jing.yandex-team.ru/files/cheetah/2022-03-23T14%3A26%3A47Z.051e585.png =x250){: .center} 
   
   1.4. Зайдите по ssh на свой дев в папку с инстансом.
   
   1.5. Выполните команду ```make madm-agent madm-agent-restart```

   1.6. Добавьте в options в madm инстанса поле madm_server_configuration со следующим значением:
   ```
   	{"instance": "<инстанс вида v190d0, откуда будут забираться экспорты из тестинга>", "pr_number": "<pr из пункта 1.3>"}
   ``` 
   
2. Используя rsync.

   1. На деве нужно создать/отредактировать файл ``/etc/rsyncd.conf`` с содержанием:
    ```
    pid file = /var/run/rsyncd.pid
    log file = /var/log/rsync/rsync.log

    use chroot = yes
    #max connections = 4

    [madm]
            path = /opt/www/bases/madm
            read only = true
            uid = morda
            gid = www-data
            comment = madm dat
    ```
   2.2. Запустить демон ``rsync``
    ```
    sudo /etc/init.d/rsync start
    ```
   2.3. Эскпорт может перетереться, если за время тестирования, он обновится в проде. Чтобы избежать этого, на деве можно отключить скрипты, которые запускаются по крону: в файле ``/etc/cron.d/morda`` закомментировать строки для скриптов ``.../scripts/get_ready_fast`` и ``.../scripts/get_ready``.
   
   2.4. На дев-инстансе отредактировать в МАДМ нужный экспорт и отправить его в ``production``. Можно убедиться, что изменения доехали в нужную папку. Пример для экспорта ``options``:
    ```
    grep my_new_option /opt/www/bases/madm/production/options
    ```
   2.5. Зайти на под беты по ssh: в Яппи беты в разделе Components есть сылка на Няню, в Няне справа выбрать ``View Pods`` и посмотреть ``FQDN`` пода.
   
   2.6. На бете в файле ``/opt/www/bases/get_madm.sh`` нацелить ``rsync`` на свой дев. 
    Пример: 
    ```
    #!/bin/bash

    rsync -r --archive --compress --verbose --include='/production' --include='/production_ready' --include='/testing' --include='/testing_ready' --exclude='/*' --delete rsync://v199.wdevx.yandex.net/madm/ /opt/www/bases/madm/
    ```
   2.7. Скрипт запускается раз в минуту. Если вы торопитесь, посмотрите от какого пользователя запускается скрипт:
    ```
    grep get_madm.sh instancectl.conf
    ```
    На момент написания документации запустить можно было так
    ```
    sudo -u www-data /bin/bash /opt/www/bases/get_madm.sh
    ```
   2.8. Экспорты с дев-инстанса должны приехать на бету.
    ```
    grep my_new_option /opt/www/bases/madm/production/options
    ```

### Как получить верстку из другой беты:
Для походов за версткой блоков ПП в графах Морды используются бэкенд ``MORDA__MORDA_DIV_RENDERER``.
На бетах этот бэкенд работает на порту 10103
Пример:
```
srwcrw=MORDA__MORDA_DIV_RENDERER:<<хост беты>>t:10103:10s
```

