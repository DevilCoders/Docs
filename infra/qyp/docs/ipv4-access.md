# Доступ к ВМ по ipv4

Внутри Яндекса доступ до всех ресурсов осуществляется только через ipv6. Однако, в ряде исключительных случаев возможно использовать ipv4, для таких случаев сделана данная инструкция.

{% note alert %}

**Обязательно сообщите [frolstas@](https://staff.yandex-team.ru/frolstas) или [alonger@](https://staff.yandex-team.ru/alonger) если считаете, что вам нужны такие доступы**!

{% endnote %}

## Настройка доступа во внешний интернет (ipv4) в Windows {#steps}

### Создать ВМ в QYP {#create-vm}

Требования к образу ВМ:
* ядро >= 3.19
* пакет iproute2 версии >= 3.18

Подробнее <https://wiki.yandex-team.ru/noc/slb-tun-rssetup/>


### Создать L3 балансер {#create-l3}

В качестве real servers балансер будет использовать [endpoint_set](https://wiki.yandex-team.ru/yp/discovery/), который придется создать вручную и привязать к балансеру через awacs. Это необходимо для решения проблемы с переездом ВМ и изменением ее сетевого адреса. Awacs подхватит изменение и обновит конфигурацию балансера.

1. [Создать сервис на l3.tt.yandex-team.ru](https://l3.tt.yandex-team.ru/service)
    Добавить new virtual server:


    ```
    IP: Get new IP
    порт и протокол сервиса: 80/tcp, 443/tcp (указать порты, которые нужны)
    описание проверки рилов: CHECK=TCP_CHECK
    Real Server в RS config: (указать выданный hostname, например my-shiny-vm.vla.yp-c.yandex.net)
    ```

2. Создать endpoint set
    Создание проще всего сделать через `yp cli`, который встроен в `ya tool`. В команде создания нужно указать кластер, где находится ВМ, имя ВМ и порт, в который будет ходить балансер.
    
    ```
    $ ya tool yp create endpoint_set --address "КЛАСТЕР-где-живет-VM" \
      --attributes '{"meta"={"id"="ИМЯ-ВМ-backend";};"spec"={"pod_filter"="[/meta/pod_set_id] = \"ИМЯ-ВМ\"";"port"=ПОРТ;"protocol"="TCP"};}'
    ```
3. Создать пустой namespace в awacs <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/create-empty/> Если планируется заведение нескольких балансеров, их можно поместить в один namespace, создавать каждый раз новый необязательно.
4. Создать в namespace новый бэкенд, привязать созданный во 2-м шаге endpoint_set. Понадобится кластер и id endpoint_set (`ИМЯ-ВМ-backend`). Type: YP endpoint sets (slow, for L3 and DNS).
5. Привязать существующий L3 балансер, в качестве бэкенда указать привязанный endpoint_set ([инструкция](https://wiki.yandex-team.ru/awacs/tutorial/L3/#add), комментарий про L3+L7 игнорировать, туннели будут настроены в следующем шаге).


### Поднять туннель внутри ВМ {#tun}

Все действия выполняются внутри ВМ:

```bash
$ svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/infra/qyp/scripts/qyp-slb-tun > qyp-slb-tun
$ chmod +x qyp-slb-tun 
$ sudo ./qyp-slb-tun start
# если нужно поднимать туннель автоматически при каждом запуске вм, добавить
$ sudo ln -s <full_path_to_script>/qyp-slb-tun /etc/network/if-up.d/qyp-slb-tun
```

### Получить доступ к ВМ {#access}

Для доступа к ВМ по v4 нужно:
1. [Добавить](https://wiki.yandex-team.ru/awacs/tutorial/L3/#dns) запись об адресах балансера в dns.
2. Получить через [puncher](https://puncher.yandex-team.ru/) доступ до fqdn L3-балансера.

