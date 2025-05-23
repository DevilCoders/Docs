#  Настройка shard'а

##  Что это такое {#what-is-shard}

Shard (шард) — это понятие системы выкладки (т.е. bsconfig).
Прямое назначение шарда — это хранение и распространение куска поисковой базы. Так у каждого инстанса базового может быть разный шард.
Каждый инстанс сервиса может иметь 1 _шард_. На диске шард представляет собой каталог и (опционально) скрипт, который необходимо запустить для установки шарда (например, распаковать какие-либо файлы). Ввиду ограничений системы, (почти) единственный способ доставить для инстанса каталог — это:

* Позвать на каталоге команду `bsconfig shard_init` (например, при сборке в Sandbox).
* Указать его в качестве шарда для требуемого инстанса.
Система поддерживает такой механизм, позволяя для удобства указывать атрибуты ресурса в Sandbox, которые она самостоятельно преобразует в нужный идентификтор шарда и укажет системе выкладки доставить его на машину при подготовке инстанса.

Рассмотрим доступные типы шардов, которые можно назначить сервису. Все изменения в UI производятся на странице Shard. После изменения необходимо нажать кнопку Save в разделе Runtime.

![img](https://jing.yandex-team.ru/files/sshipkov/service_shard_page.0d75fdc.png)

##  Локальный путь к шарду {#shard-local-path}
При использовании bsconfig в качестве системы выкладки шард всегда находится в определённом каталоге, вне каталога инстанса. Например, `/db/BASE/primus-Tur0-8-23-1431890942`. Это позволяло использовать один шард в нескольких инстансах.
При использовании ISS в качестве системы выкладки шард — это тип ресурса, который вместе с остальными проецируется (через символьные ссылки) в каталог инстанса. Путь можно указать в поле **Local path**. При использовании bsconfig это поле будет игнорироваться.

##  Ресурс Sandbox — SANDBOX_SHARD {#sandbox-shard}
В выпадающем списке выбираем `SANDBOX_SHARD` и с помощью интерактивной подсказки указываем нужные параметры:

* Task Type — типа задачи в Sandbox
* Task Id — идентификатор задачи (предлагается выбор из нескольких самый свежих)
* Resource type — тип ресурса задачи (задача может породить несколько ресурсов)

{% note warning %}

Система рассчитывает, что при выполнении кода задачи шард был проинициализирован в выбранной системе выкладки — Bsconfig или ISS.

{% endnote %}

##  Идентификатор шарда — REGISTERED_SHARD {#registered-shard}
Позволяет указать произвольный идентификатор шарда, созданный не в Sandbox. Система рассчитывает, что шард был создан пользователем самостоятельно.

##  Ресурс Sandbox с shardmap'ом — SANDBOX_SHARDMAP {#sandbox-shardmap}
Shardmap — в поиске это способ описать поколение поисковой базы. В общем виде содержит список строк вида:

```
<instance_info> <shard_info> < [...] shard_tags>
```
1. Instance info может быть как парой хост:порт, так и виртуальным шардом:

    * Если в начале идёт указание "host_port", то структура должна быть "host_port:<host>:<port>"
    * Если в начале идёт указание "pod_id", то структура должна быть "pod_id:<pod_id>"
    * Если в начале идёт указание "pod_label", то структура должна быть "pod_label:<label_key>=<label_value>"
    * В остальных случаях весь <instance_info> воспринимается как virtual shard (виртуальный шард — идентификатор шарда без указания поколения базы).
    
    Примеры:
    ```
    host_port:vla1-1414.search.yandex.net:2184
    pod_id:kggwuqefk6zlmfgq
    pod_label:awesome_label=some_value
    imgfidx-000-00000000-000000
    ```

2. Shard info может быть указан или с помощью rbtorrent_url, или как shard_id из шардтрекера (идентификатор шарда в указанном поколении базы). Также это может быть resourceless_shard_id, который не приносит ресурc на машину, а служит только для разметки.

    * Если в начале идёт "rbtorrent", то структура должна быть "rbtorrent:<rbtorrent_url>"
        Также можно опционально указать local path файла: "rbtorrent:<rbtorrent_url>(local_path=<local_path>)"
    * Если в начале идёт "resourceless_shard_id", то структура должна быть "resourceless_shard_id=<id>".
    * В остальных случаях <shard_info> воспринимается как shard_id.
        В этом случае также опционально можно указать source_host: "<shard_id>(srchost=<source_host>)"

    Примеры:
    ```
    rbtorrent:12345567789sdf
    rbtorrent:agfosi87235jbh(local_path=some_local_path)
    resourceless_shard_id=not_a_resource_1
    primus-Rus-1-3-5-1431890942
    imgfidx-000-20151015-151602(srchost=pi00)
    ```


3. Shard tags состоит из любого количества тэгов, разделенных пробелами. Тэг шарда — это строка, описывающая тип шарда (например, шард турецкой базы).
