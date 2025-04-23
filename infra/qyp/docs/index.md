# QYP

**QYP** — это система виртуализации QEMU-KVM, работающая поверх существующей инфраструктуры [Runtime Cloud](https://rtc.yandex-team.ru/docs/).

## Миссия {#mission}

QYP предназначен для запуска и управления виртуальных машин (далее ВМ), используемых для задач разработки, а также развертывания агентов систем continuous integration.

{% note alert %}

QYP **не предназначен** для развертывания продакшн сервисов, для этих целей существуют специализированные системы [Nanny](https://wiki.yandex-team.ru/runtime-cloud/nanny/), [Qloud](https://wiki.yandex-team.ru/qloud/), реализующие различные политики деплоя приложений, обеспечивающие учет degrade level, работу с балансерами и многое другое.

{% endnote %}

## Цели QYP {#goals}

* Возможность запуска в Runtime Cloud ВМ с кастомными образами/операционными системами (Linux, Windows, Android, etc).
* Быстрое создание ВМ в облачной инфраструктуре.
* Возможность кастомного менеджмента поднятых виртуалок.

## Планы по развитию {#plans}

[QYP. Планы](https://wiki.yandex-team.ru/qyp/plans/)

## Общее описание системы {#common}

Гипервизор работает на основе [QEMU](https://wiki.qemu.org/Main_Page) (Quick EMUlator) используемого в качестве системы виртуализации и модуля ядра Linux [KVM](http://www.linux-kvm.org/page/Main_Page) для повышения производительности QEMU. VM настраивается с помощью диска с конфигом для [cloud-init](http://cloudinit.readthedocs.io/) в формате nocloud. Конфигурация сети аналогична MTN ([Multi Tennancy Network](https://wiki.yandex-team.ru/andrejjabroskin/archive/mtn-post-may-2018/)) сети контейнеров и прозрачно интегрирована с [HBF](andrejjabroskin/archive/mtn-post-may-2018/).

Основной feature set:

* [QYP UI](ui.md).
* [CLI для работы с виртуальными машинами](cli.md).
* [Базовый набор образов](images-set.md), в том числе `"devel"` образа с предустановленным набором пакетов для разработки.
* [Поддержка CAuth](https://clubs.at.yandex-team.ru/infra-cloud/46).
* NoVNC.
* Поддержка доступа в Интернет:
   * [NAT64/DNS64](https://clubs.at.yandex-team.ru/infra-cloud/70).
   * [Туннели](https://clubs.at.yandex-team.ru/infra-cloud/62).
* Возможность [бэкапов ВМ](https://clubs.at.yandex-team.ru/infra-cloud/145).
* Возможность [работы с sandox в виртуалке](https://st.yandex-team.ru/QEMUKVM-22#1518691140000).
* [Возможность мониторинга](https://clubs.at.yandex-team.ru/infra-cloud/60) контейнеров с ВМ, а также набора сигналов с unistat-ручки, характеризующий состояние ВМ при помощи Golovan.


### Схема использования {#scheme}

#### QEMU-KVM over YP {#scheme-qemu-vkm-over-yp}

Аллокация ресурсов переводится при помощи планировщика [Yandex Planner (YP)](https://wiki.yandex-team.ru/yp/).

## Схема решения {#solution}

![](_assets/structure.png)

**Как начать работу с ВМ**

* [Получить квоту в YP](https://wiki.yandex-team.ru/yp/quotas/), либо воспользоваться аккаунтом *tmp* для ознакомления;
* [Создать ВМ в UI](ui.md), либо [создать ВМ при помощи CLI](cli.md).

## Описание Workflow {#workflow}

1. Пользователь отправляет запрос на аллокацию pod'ов через vmproxy, указывая в параметрах требуемые параметры:
    * cpu_guarantee
    * cpu_limit
    * ram_guarantee
    * ram_limit
    * образ диска
    * список пользователей-админов
    * сегмент оборудования (`dev `|` default`)
2. vmproxy проверяет запрошенные параметры аллокации:
   
    Если выбран dev:
    * Если `cpu_guarantee > 2c`, то выводим сообщение об ошибке (`cpu_guarantee` до внедрения квот не должен превышать 2 ядра в сегменте dev).
    * `cpu_limit` не лимитируем (может быть равным cpu хоста). Для прочих сегментов:
      * `cpu_guarantee` — определяется пользователем;
      * `cpu_limit` — определяется пользователем;
    * отправляет запрос на аллокацию в YP
3. YP аллоцирует ресурсы, возвращая набор pod'ов (podset) с соотв. набором pod_id
4. vmproxy, после получения статуса об успешной аллокации:
    * формирует конфигурацию (payload) сервиса;
    * запрашивает со staff публичные ключей пользователей, обладающих правом управления podset'ом;
    * зашивая в annotations информацию о составе пользователей, обладающих правом управления podset'ом; размещая ssh ключи указанных пользователей в подах;
    * отправляет запрос на аллокацию в YP, аутентифицируясь при помощи клиентского сервисного сертификата;
5. YP передает полученный payload/конфигурацию в ISS Agent, размещенные на целевых хостах;
6. ISS Agent создает pod'ы указанной конфигурации, скачивая указанные в качестве ресурсов образы.

**Операции с pod'ами**

1. Старт виртуалки.
1. Изменение состояния виртуалки.
1. Получение статуса виртуалки.

### Компоненты {#components}

* `kvm-novnc`. В Runtime Cloud поднят Nanny-сервис [kvm-novnc](https://nanny.yandex-team.ru/ui/#/services/catalog/kvm-novnc/) на инстансах которого подняты следующие компоненты сервиса QEMU-KVM:
    * [vmproxy](https://wiki.yandex-team.ru/qyp/API-CLI/), [vmctl](https://wiki.yandex-team.ru/qyp/API-CLI/) — реализуюют API и CLI к qemu виртуалкам. Доступ к API осуществляется через сервисный балансер <https://rtc-kvm-vmproxy.n.yandex-team.ru>, параметры запросов описаны [в документации](https://wiki.yandex-team.ru/qyp/API-CLI/).
    * [NoVNC](https://github.com/novnc/noVNC) — VNC клиент для доступа к qemu-виртуалке через браузер. Доступ осуществляется через L3-балансер, точка входа <https://rtc-kvm-novnc.yandex-team.ru/vnc.html>, параметры запросов описаны [в документации](https://wiki.yandex-team.ru/qyp/API-CLI/#vnc-dostup).
* `portoshell` — cтандартный инфраструктурный сервис, предоставляющий возможность взаимодействовать с vmctl, который получает порт инстанса из env и пытается соединиться с локальным vmagent.
* `vmagent` — Python-библиотека реализующая управляющие операции с виртуалками (push_config/start/reboot/shutdown/reset/poweroff/hard_reset/snapshot), а также функционал получения статуса виртуалок.

### Документация {#docs}

**YP-based аллокации**
* [QYP: Помощь по UI](ui.md)
* [QYP: Помощь по CLI](cli.md)


**Разное**
* [Работа со snapshots в ручном режиме](https://wiki.yandex-team.ru/qyp/manual-snapshotting/)
* [Образы QEMU_IMAGE_SEARCH для виртуальных машин в RTC](images-set.md)
* [Миграция из OpenStack в RTC](https://wiki.yandex-team.ru/qyp/os-migration/)
* [Рецепты по исправлению проблем](troubleshooting.md)
* [Процедура настройки доступа во внешний интернет (ipv4) в Windows](ipv4-windows.md)


### Накладные расходы {#performance}

Результаты тестов по сборке Аркадии по сравнению с железными машинками приведены [здесь](https://wiki.yandex-team.ru/qyp/testing/performance/).


### Исходный код {#source}

* [vmagent](https://a.yandex-team.ru/arc/trunk/arcadia/infra/qyp/vmagent)
* [vmctl](https://a.yandex-team.ru/arc/trunk/arcadia/infra/qyp/vmctl/)
* [vmproxy](https://a.yandex-team.ru/arc/trunk/arcadia/infra/qyp/vmproxy)
* [QDM](https://a.yandex-team.ru/arc/trunk/arcadia/infra/qyp/qdm)
* [UI](https://bb.yandex-team.ru/projects/NANNY/repos/qyp.ui/browse)


### Сборка и выкладка новой версии {#release}

См. [QEMU-KVM: Сборка и выкладка новой версии](https://wiki.yandex-team.ru/qyp/release/)


## Тестирование {#testing}

[QYP. Тестирование](https://wiki.yandex-team.ru/qyp/testing/)


## Администрирование и поддержка {#support}

### Инсталляции {#installations}

#### QEMU-KVM over YP {#inst-qemu-kvm-yp}

Для аллокации доступна часть кластера RTC, находящаяся под контролем YP.

##### Сегменты {#inst-segments}

1. **default**
   Сегмент предназначен для "сервисных" ВМ (CI/CD). См. [Кластеры оборудования](https://wiki.yandex-team.ru/yp/klastery/).

1. **dev**
   Сегмент предназначен для размещения виртуальных машин для разработки, спецификой является отсутствие лимита по CPU на ВМ (CPU лимитирован ресурсами железной машины за вычетом накладных расходов на инфраструктуру).
1. **gpu-dev**
   Сегмент предназначен для размещения виртуальных машин для разработки, как и сегмент **dev**. Отличие в том, что в **gpu-dev** можно заказывать ВМ только с GPU

См. [QYP. Оборудование](https://wiki.yandex-team.ru/qyp/hardware/)


### Мониторинги {#monitorings}

* [Сервис мониторинга сломанных виртуалок](https://wiki.yandex-team.ru/qyp/pod-alive-monitoring/)
* [Статистика по QEMU VM/QYP](https://yasm.yandex-team.ru/panel/qemu)
* [Потребление квоты в Sandbox группой QEMU_BACKUP](https://grafana.yandex-team.ru/d/000015873/sandbox-quota-consumption-production?refresh=1m&orgId=1&var-owner=QEMU_BACKUP)
* [Вызовы методов API](https://yasm.yandex-team.ru/chart/itype=unknown;prj=vmproxy;hosts=ASEARCH;ctype=prod;signals=%7Bunistat-services-http-rpc-vmset-service-GetStatus-count_summ,unistat-services-http-rpc-vmset-service-ListYpVm-count_summ,unistat-services-http-rpc-vmset-service-ListUserAccounts-count_summ,unistat-services-http-rpc-vmset-service-ListBackup-count_summ,unistat-services-http-total-count_summ,unistat-services-http-rpc-vmset-service-CreateVm-count_summ%7D;geo=sas/)

Состояние хостов сегмента `YP.dev`:

* [VLA](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/project=yp-iss-vla-dev;ctype=prod)
* [SAS](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/project=yp-iss-sas-dev;ctype=prod)
* [MAN](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/project=yp-iss-man-dev;ctype=prod)

vmproxy

* [Метрики с балансера](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/prj=swat,iva-swat.yandex-team.ru,myt-swat.yandex-team.ru;signal=production-vmproxy;locations=sas,man,vla,msk/)
* [Vmproxy Api Clients Timings](https://yasm.yandex-team.ru/panel/i-dyachkov.qyp.vmproxy-clients-timings)
* [алерты на OOM и CPU](https://yasm.yandex-team.ru/template/alert/vmproxy/)

vmagent

* [Метрики сетевой доступности ВМ](https://yasm.yandex-team.ru/chart/hosts=ASEARCH;itype=qemuvm;ctype=prod;signals=%7Bunistat-link_alive_ammv,unistat-net_alive_ammv%7D/). Раз в секунду vmagent отправляет запросы ping и connect на 22 порт (SSH) к запущенной ВМ, результат транслируется в link_alive и net_alive соответственно
* [Версии vmagent на кластере](https://yasm.yandex-team.ru/panel/VMAGENT_VERSIONS)


## Поддержка {#support}

Поддержка осуществляется через [telegram-чат rtc-support](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q).


## Рецепты по исправлению проблем {#troubleshooting}

[QYP. Рецепты по исправлению проблем](troubleshooting.md)

