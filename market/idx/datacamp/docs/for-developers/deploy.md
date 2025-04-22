# Храниилище + YD

Сервисы хранилища в YD: [https://deploy.yandex-team.ru/projects/market-datacamp](https://deploy.yandex-team.ru/projects/market-datacamp)

## Терминология
* Workload — одна секция с запуском команды/бинарника
* Box — изолированный контейнер
* Pod — один хост, в котором запускается приложение
* Deploy unit — группа подов
* Stage — один микросервис в одном из окружений
* [Более подробно](https://deploy.yandex-team.ru/docs/launch/#struktura-servisa-v-deploy)

{% cut "Страница сервиса" %}

![pic](../_images/deploy_main.png)

{% endcut %}

## Как подключиться по ssh
1. Выбираем хост
2. Копируем команду из UI для поключения к боксу
3. К Pod нельзя подключаться!

{% cut "Картиночка" %}

![pic](../_images/deploy_pod_info.png)

{% endcut %}

## Расположение файлов в ФС
Обычный сервис:
```
/app                 # Директория для приложения
|--/bin              # Для исполняемых файлов, например sh-ников, скомпилированных бинарей
|--/conf             # Директория для хранения конфигов приложения
|--/cache            # сюда кладем то, что не страшно снести в любой момент
|--/cores            # сюда будут валиться корки
|--/lib              # Библиотеки для работы приложений, если нужны
|--/log              # Директория с линками в /var/log/yandex
|--/jdk              # сюда кидаем jdk, если у нас java приложение
|--/datasources       # здесь будут жить датасорсы
|--/run              # аналогично /var/run или /run
|--/data             # сюда кладем такое, что регулярно меняется и требует сохранности между рестартами, а-ля /var/lib
|--/secrets          # каталог с файлами, приезжающими из секретницы
|--/static           # различные css, js и т.д. скрипты. 
|--/tmp              # собственно /tmp
```

SOX-сервис:
```
/sox                 # RO-фс
|--/app              # распакованный пакет с приложением
|----/bin
|----/etc
|----/static
/app
|--/cache            # сюда кладем то, что не страшно снести в любой момент
|--/cores            # сюда будут валиться корки
|--/etc              # RW копия из /sox/app/etc
|--/lib              # Библиотеки для работы приложений, если нужны
|--/log              # Директория с линками в /var/log/yandex
|--/run              # аналогично /var/run или /run
|--/data             # сюда кладем такое, что регулярно меняется и требует сохранности между рестартами, а-ля /var/lib
|--/secrets          # каталог с файлами, приезжающими из секретницы
|--/tmp              # собственно /tmp
```

## Как залить свой пакет с бинарником в обход ЦУМа
SOX сервис пока что можно обновить только через редактирование спеки сервиса через YAML-конфиг.
0. Собрать свой пакет с приложением. ВАЖНО: пакеты для YD и Nanny различаются
1. Получить текущую спеку сервиса `ya tool dctl get stage testing_market_datacamp-miner-msku > my_new_spec.yaml`
2. Поменять в спеке ресурса `application`
3. Запушить изменения спеки `ya tool dctl put stage my_new_spec.yaml`

## Как долить железа в сервис
{% cut "1. Открыть настройки deploy unit" %}

![pic](../_images/deploy_edit_service.png)

{% endcut %}

{% cut "2. Увеличить количество хостов/ресурсов" %}

![pic](../_images/deploy_resources.png)

{% endcut %}

{% cut "3. Сохранить изменения" %}

![pic](../_images/deploy_save.png)

{% endcut %}

## Графики утилизации
На странице сервиса вкладка Monitoring. 

## ITS
Настроен отдельный workload, который поллит данные из its няни

## Множественные операции aka sky run {#sky}
[Анонс поддержки sky в YD](https://clubs.at.yandex-team.ru/infra-cloud/1271)

В целях ограничения доступа до продовых контейнеров, доступ через `sky` возможен только с мастеров индексации(mi01ht, mi01h, mi01v),
с разработческих машин есть доступ только до тестинга. Во всех стейджах хранилища придерживаемся правила,
что боксы с приложением называются `application_box`, тогда команда запуска будет выглядеть следующим образом:
```
sky run --user nobody 'uptime' b@market-datacamp.<stage>.<deploy-unit>.application_box

sky run --user nobody 'uptime' b@market-datacamp.testing_market_datacamp-miner.miner.application_box
```

По-умолчанию рекомендуется выполнять команды под бесправным пользователем `nobody`, например если надо погрепать логи. Если надо покилять процессы, то запускаем под пользователем root и получаем в подарок тикет в очереди SECALERT.

#### Я получаю ошибку Host is silent
Скорее всего, нет дырок до подов. Запускаешь с мастера индексации? Проверь сетевые доступы в [puncher](https://puncher.yandex-team.ru): 
[https://deploy.yandex-team.ru/docs/concepts/pod/box#setevye-dostupy-dlya-skynet](https://deploy.yandex-team.ru/docs/concepts/pod/box#setevye-dostupy-dlya-skynet).
В проде сетевой макрос `_MARKET_PROD_INDEXER_NETS_`, в тестинге — `_MARKET_TEST_INDEXER_NETS_`.

Вторая возможная причина — на подах не запущен `sky`, [как включать](https://deploy.yandex-team.ru/docs/concepts/pod/box#setevye-dostupy-dlya-skynet).

#### Я получаю ошибку No private keys available. Cannot run the task
Скорее всего, при подключении к мастеру индексации не пробросились ключи. Переподключись с agent-forwarding `ssh -A mi01h.market.yandex.net`.
Если не помогло, то попробуйте `ssh-agent && ssh-add && ssh -A mi01h.market.yandex.net`

## Как подключиться к поду зная ipv6
```(bash)
> host 2a02:6b8:c08:8986:0:5275:4345:0
0.0.0.0.5.4.3.4.5.7.2.5.0.0.0.0.6.8.9.8.8.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa domain name pointer qrrltl7sf7dtmucn.sas.yp-c.yandex.net.
> ssh nobody@application_box.qrrltl7sf7dtmucn.sas.yp-c.yandex.net

> host 2a02:6b8:c08:8986:0:5275:4345:0 | awk '{print "ssh nobody@application_box."$NF}'
```

## Как найти стейдж зная ipv6
1. Из `host 2a02:6b8:c08:8986:0:5275:4345:0` получаем pod_id, например `qrrltl7sf7dtmucn`
2. С этим pod_id идем в [https://deploy.yandex-team.ru/yp](https://deploy.yandex-team.ru/yp)

## Агрегация корок
На контейнерах корки сохраняются в директорию `/coredumps_box`, на контейнере хранится не более двух корок. При этом новая корка
может не сохраниться, если самая старая корка произошла в течение последнего получаса. Также корки агрегируются в сервисе
[три корочки](https://wiki.yandex-team.ru/cores-aggregation/):
* [miner](https://coredumps.yandex-team.ru/index?itype=datacamp_miner_workload)
* [piper](https://coredumps.yandex-team.ru/index?itype=datacamp_piper_workload)
* [scanner](https://coredumps.yandex-team.ru/index?itype=datacamp_scanner_workload)
* [stroller](https://coredumps.yandex-team.ru/index?itype=datacamp_stroller_workload)
* [parser](https://coredumps.yandex-team.ru/index?itype=datacamp_parser_workload)
* [checkfeed](https://coredumps.yandex-team.ru/index?itype=datacamp_checkfeed_workload)
* [routines](https://coredumps.yandex-team.ru/index?itype=datacamp_routines_workload), только то, что запускается в YD. Корки sandbox тасок прикапываются непосредственно к самой таске.

## Ссылки
* [Основная документация по YD](https://deploy.yandex-team.ru/docs/)
* [FAQ от команды MBI](https://wiki.yandex-team.ru/mbi/development/howto/faq-po-ja.deplojj/)
* [Как маркет будет переезжать в деплой[1]](https://wiki.yandex-team.ru/market/sre/fordev/dyp/relocation/)
* [Как маркет будет перезжаать в деплой[2]](https://wiki.yandex-team.ru/market/sre/kak-market-poedet-v-deplojj/)
