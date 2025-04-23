# Базовый набор образов

Это уже готовые образы для работы, адаптированные для работы в RTC. Можно использовать как непосредственно сами ресурсы (со статусом RELEASED), так и использовать их как образцы для варки собственных образов с использованием Sandbox.

## Типы образов {#types}

### Базовый образ {#base}

* [xenial](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_RTC_UBUNTU_XENIAL&owner=RCCS-ADMINS&state=READY) - **16.04**
   
   {% cut "список пакетов" %}
   
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-xenial/script/42_base_tools.sh>
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-xenial/script/43_admin_tools.sh>
   
   {% endcut %}

* [bionic](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_RTC_UBUNTU_BIONIC&owner=RCCS-ADMINS&state=READY) - **18.04**
   
   {% cut "список пакетов" %}
   
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-bionic/script/42_base_tools.sh>
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-bionic/script/43_admin_tools.sh>
   
   {% endcut %}

* [focal](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_RTC_UBUNTU_FOCAL&owner=RCCS-ADMINS&state=READY) - **20.04**
   
   {% cut "список пакетов" %}
   
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-focal/script/42_base_tools.sh>
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-focal/script/43_admin_tools.sh>
   
   {% endcut %}


### Образ для разработчиков {#dev}

* [xenial-dev](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_RTC_UBUNTU_XENIAL_DEVEL&owner=RCCS-ADMINS&state=READY) - **16.04**
   
   {% cut "список пакетов" %}
   
   пакеты из базового образа xenial (см выше) +
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-xenial/script/46_dev_tools.sh>
   
   {% endcut %}

* [bionic-dev](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_RTC_UBUNTU_BIONIC_DEVEL&owner=RCCS-ADMINS&state=READY) - **18.04**
   
   {% cut "список пакетов" %}
   
   пакеты из базового образа bionic (см выше) +
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-bionic/script/46_dev_tools.sh>
   
   {% endcut %}

* [focal-dev](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_RTC_UBUNTU_FOCAL_DEVEL&owner=RCCS-ADMINS&state=READY) - **20.04**
   
   {% cut "список пакетов" %}
   
   пакеты из базового образа focal (см выше) +
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-focal/script/46_dev_tools.sh>
   
   {% endcut %}

{% note info %}

В случае необходимости расширения состава пакетов в dev-образах, необходимо завести тикет с запросом на это в очереди [st/RTCSUPPORT](https://st.yandex-team.ru/createTicket?queue=RTCSUPPORT)

{% endnote %}


### Образ для разработки с GPU {#with-gpu}

* [xenial-gpu](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_SEARCH_XENIAL_GPU_DEVEL&owner=RCCS-ADMINS&state=READY&limit=20) 
   
   {% cut "список пакетов" %}
   
   пакеты из dev образа xenial (см выше) + установлены драйвера nvidia и cuda
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-xenial/deploy-cuda.sh>
   
   {% endcut %}
   
* [bionic-gpu](https://sandbox.yandex-team.ru/resources?type=QEMU_IMAGE_SEARCH_BIONIC_GPU_DEVEL&owner=RCCS-ADMINS&state=READY&limit=20) 
   
   {% cut "список пакетов" %}
   
   пакеты из dev образа bionic (см выше) + установлены драйвера nvidia и cuda
   <https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/rtc-base-bionic/deploy-cuda.sh>
   
   {% endcut %}


### Windows {#windows}

Готовых образов для запуска Windows в контейнерах у нас нет. Можно взять образ из OpenStack и залить в Sandbox ([как посмотреть](https://wiki.yandex-team.ru/iaas/clients/#poluchitspisokpodderzhivaemyxnamiobrazov), [как залить](https://wiki.yandex-team.ru/yatool/upload/))


## Технические детали {#details}

Варим образы с помощью Sandbox Task **YA_MAKE_TGZ**, два раза в неделю с помощью [Sandbox шедулера](https://sandbox.yandex-team.ru/schedulers?page=1&pageCapacity=20&order=-id&task_type=YA_MAKE_TGZ&recipients=&owner=RCCS-ADMINS)

Образы собираются на базе аркадийного инструментария [infra/environments](https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments) и названы там `rtc-base-<osrelease_codename>`. Скрипты, которые выполняются в chroot для сборки/настройки образа находятся в `infra/environments/rtc-base-<osrelease_codename>/scripts`.
