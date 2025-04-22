# Мониторинг через yasm/golovan

[Основной HOWTO для настройки мониторинга](https://wiki.yandex-team.ru/golovan/golovan-howto/).

[Я всё сделал, но у меня нет сигналов, что делать?!](https://wiki.yandex-team.ru/golovan/no-signals-checklist/)

Ниже описаны шаги, необходимые для мониторинга через yasm (golovan):

1. Метрик потребления ресурсов инстансами: CPU, RAM, network, etc.
1. С помощью [unistat-ручки](https://wiki.yandex-team.ru/golovan/stat-handle/#format) и числа возвращаемых сигналов **меньше 1000**;
1. С помощью [unistat-ручки](https://wiki.yandex-team.ru/golovan/stat-handle/#format) и произвольного числа возвращаемых сигналов (на самом деле есть некая большая константа в головане, в которую вы вряд ли упрётесь).

Ключевой момент в настройке мониторинга — выбор `itype` и `prj` инстанса. `itype` определяет способ, которым yasm-agent на конкретном хосте кластера будет получать метрики инстанса. Возможные варианты того, что может делать yasm-agent: собирать метрики потребления контейнера, обращаться к unistat-ручке инстанса по HTTP, парсить логи инстанса и т.п. Типичные значения для `itype`: `mongo`, `zookeeper`, `basesearch`, т.е. обычно это типы программ.

При деплое на YP_LITE `itype` указывается в сервисе Nanny. Если вам достаточно мониториться дефолтным способом (через [стат-ручку](https://wiki.yandex-team.ru/golovan/stat-handle/) с количеством сигналов не более 1000 или [push api](https://wiki.yandex-team.ru/golovan/push-api/) + стандартные метрики потребления ресурсов контейнером), то больше ничего делать не надо. В противном случае необходимо завести в [репозитории голована](https://bb.yandex-team.ru/projects/SEARCH_INFRA/repos/yasm/browse/CONF/) конфиг с настройками вашего мониторинга (подробнее про его формат — [здесь](https://doc.yandex-team.ru/Search/golovan-quickstart/concepts/agent-config.html)).

Важно помнить, что при наличии нескольких инстансов с одинаковыми значениями всех тэгов `itype`, `ctype`, `prj` и других на одном хосте, значения их сигналов будут сагрегированны (например, просуммированы) и посмотреть их по отдельному инстансу не удастся, т.к. yasm обязательно агрегирует все сигналы при совпадении всех тэгов. Поэтому для того, чтобы избежать склеивания значений своих сигналов с соседями, достаточно указать своё уникальное значение тэга `prj`, чтобы сигналы инстанса гарантированно не были сагрегированны с сигналами соседей, у которых выставлено дефолтное значение `prj = none`.

## Мониторинг потребления ресурсов контейнером через yasm/golovan {#yasm-monitoring-container}

Рядом с инстансом нажать ссылку YASM, чтобы увидеть графики потребления ресурсов.

## Мониторинг с помощью unistat с малым числом сигналов {#yasm-monitoring-rtcsmall}

Если вас не интересует никакой мониторинг кроме потребления ресурсов и unistat-ручки или посылки сигналов через push api Голована, и число сигналов unistat-ручки **меньше 1000**, то для их включения достаточно:

1. В Няне во вкладке Инстансы поставить необходимые теги;
1. Создать пустой контейнер **с именем существующей секции в instancectl.conf** или использовать существующий [(подробнее об использовании контейнеров)](https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/howtos/structured-instancectl-config-how-to/#how-to), добавить в нем YASM unistat endpoint. Можно указать несколько адресов.
    ![yasm](https://jing.yandex-team.ru/files/sshipkov/Instance_Spec__production_nanny__Services__Home_2017-11-28_14-56-06.f9963fc.png)
1. Указать `port` (обязательно) и `path`.

    Итоговый url будет выглядеть `http://{container_ip}:{port}/{path}`, где:

    * `container_ip` — если используется mtn, backbone ip контейнера, иначе `localhost`
    * `port` — можно указывать цифры или алиасы вида `{BSCONFIG_IPORT}`, `{BSCONFIG_IPORT_PLUS_...}`
    
    ![yasm](https://jing.yandex-team.ru/files/sshipkov/Instance_Spec__production_nanny__Services__Home_2017-11-28_14-58-01.409c2ce.png)

1. Настроить в сервисе unistat-ручку, отвечающую по данному URL в соответствии с [форматом](https://wiki.yandex-team.ru/golovan/stat-handle/#format);
1. Перевыкатить сервис.

##  Мониторинг с помощью unistat с произвольным числом сигналов {#yasm-monitoring-unistat-full}

В данном случае необходимо будет завести собственный `itype` с коммитом в репозиторий yasm и ожиданием выкладки yasm-агента на кластер. [Подробный HOWTO](https://wiki.yandex-team.ru/golovan/golovan-howto/).
Крупноблочно нужно сделать следующее:

1. Закоммитить конфиг для своего `itype` в репозиторий yasm-агента со своими настройками (возможные настройки стат-ручки описаны [здесь](https://wiki.yandex-team.ru/golovan/stat-handle/#unistat-options)), пройдя процедуру ревью кода, указав в нём:

    ```
    [sources]
    unistat = unistat
    
    [options_unistat]
    max_sig_count = 2000
    url_from_iss = yasmUnistatUrl
    keep_url_port = true
    ```

2. Дождаться выкатки yasm-agent с новым `itype` на кластер.
3. Вписать созданный `itype` в сервисе;
4. Создать пустой контейнер **с именем существующей секции в instancectl.conf** или использовать существующий [(подробнее об использовании контейнеров)](https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/howtos/structured-instancectl-config-how-to/#how-to), добавить в нем YASM unistat endpoint.  Можно указать несколько адресов.
    ![yasm](https://jing.yandex-team.ru/files/sshipkov/Instance_Spec__production_nanny__Services__Home_2017-11-28_14-56-06.f9963fc.png)
5. Указать `port` (обязательно) и `path`.
    
    Итоговый url будет выглядеть `http://{container_ip}:{port}/{path}`, где

    * `container_ip` — если используется mtn, backbone ip контейнера, иначе `localhost`
    * `port` — можно указывать цифры или алиасы вида `{BSCONFIG_IPORT}`, `{BSCONFIG_IPORT_PLUS_...}`

    ![yasm](https://jing.yandex-team.ru/files/sshipkov/Instance_Spec__production_nanny__Services__Home_2017-11-28_14-58-01.409c2ce.png)

6. Настроить в сервисе unistat-ручку, отвечающую по данному URL в соответствии с [форматом](https://wiki.yandex-team.ru/golovan/stat-handle/#format);
7. Перевыкатить сервис.
