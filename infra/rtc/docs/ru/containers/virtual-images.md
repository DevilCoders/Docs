# Образы контейнеров
Команда RTC занимается сборкой и поддержкой базовых образов для запуска различного вида нагрузки - Porto, Docker, Qemu. Рекомендуется для своих нагрузок использовать именно эти базовые образы. Или же использовать их как образцы для варки собственных образов с использованием Sandbox. Если вы сомневаетесь, то используйте те образы, которые предложены по дефолту (тем самым вы поможете нам [экономить](https://warwish.at.yandex-team.ru/35) ресурсы).

## Мотивация к использованию именно этих образов
* Унификация базовых образов разных команд.
* Улучшение утилизации хостов за счет переиспользования образов.
* Безопасность. Эти образы регулярно проверяются СИБ на предмет уязвимостей.

## Существуют следующие типы образов
### Минимальный образ
{% note info %}

Рекомендуется использовать данный тип образов.

{% endnote %}

**virt_mode=app** список компонентов: [app-image](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/base-images-salt/app-image/top.sls)

* [xenial app](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_XENIAL_APP&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)
* [bionic app](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_BIONIC_APP&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)
* [focal app](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_FOCAL_APP&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)

{% cut "Deprecated" %}

* [precise app](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_PRECISE_APP&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)
* [trusty app](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_TRUSTY_APP&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)

{% endcut %}

### Расширенный образ
**virt_mode=os** список пакетов: [os-images](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/base-images-salt/os-image/top.sls)

* [xenial os (init - systemd, xenial с sysvinit более не поддерживается)](https://sandbox.yandex-team.ru/resources?attr_name=released&attr_value=stable&owner=RCCS-ADMINS&state=READY&type=PORTO_LAYER_SEARCH_UBUNTU_XENIAL&limit=20&attrs=%7B%7D&created=6_months)
* [bionic os](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_BIONIC&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released)

{% cut "Deprecated" %}

* [trusty os](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_TRUSTY&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)
* [precise os](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_PRECISE&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)

{% endcut %}

### Расширенный образ (с поддержкой субагентов)
**juggler-client**, **skynet**, **sshd** используется хостовый если в няне указать соответствующие настройки [пример](https://wiki.yandex-team.ru/runtime-cloud/nanny/howtos/juggler-subagent/)
**virt_mode=os_subagents** список пакетов: [os-sub-image](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/base-images-salt/os-sub-image/top.sls)

* [xenial os](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_XENIAL_SUBAGENT&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)
* [bionic os](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_BIONIC_SUBAGENT&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released)

{% cut "Deprecated" %}

* [trusty os](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_TRUSTY_SUBAGENT&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)
* [precise os](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=PORTO_LAYER_SEARCH_UBUNTU_PRECISE_SUBAGENT&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&recipients=&attr_name=released)

{% endcut %}

### Docker
Существуют базовые образы Ubuntu:

* `registry.yandex.net/rtc-base/xenial:stable`
* `registry.yandex.net/rtc-base/bionic:stable`
* `registry.yandex.net/rtc-base/focal:stable`

Тег stable не рекомендуется использовать т.к. нет гарантии герметичности сборки. Подробности на [отдельной странице](https://wiki.yandex-team.ru/docker-registry/#bazovyedocker-obrazy).

### QEMU
**virt_mode=qemu** список пакетов: [vm-image](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/base-images-salt/vm-image/top.sls)

* [xenial qemu systemd](https://sandbox.yandex-team.ru/resources?attr_name=released&attr_value=stable&owner=RCCS-ADMINS&state=READY&type=QEMU_IMAGE_SEARCH_XENIAL_SYSTEMD&limit=1&attrs=%7B%7D)
* [bionic qemu](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_BIONIC&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released&recipients=)

{% cut "Deprecated" %}

* [trusty qemu (deprecated)](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_TRUSTY&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released&recipients=)
* [precise qemu (deprecated)](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_PRECISE&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released&recipients=)
* [xenial qemu (deprecated)](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_XENIAL&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released&recipients=)

{% endcut %}

### Образы для dev-виртуалок QEMU
**virt_mode=qemu**  список пакетов: [common_os.sls](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/raw/search_runtime/virtual_image/common_os.sls), [common_os_with_skynet.sls](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/raw/search_runtime/virtual_image/common_os_with_skynet.sls), [common_qemu.sls](https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/raw/search_runtime/virtual_image/common_qemu.sls), [devel_packages.sh](https://a.yandex-team.ru/robots/trunk/genconf/PORTOVM/common/devel_packages.sh)

* [xenial qemu systemd devel](https://sandbox.yandex-team.ru/resources?attr_name=released&attr_value=stable&owner=RCCS-ADMINS&state=READY&type=QEMU_IMAGE_SEARCH_XENIAL_SYSTEMD_DEVEL&limit=1&attrs=%7B%7D)
* [bionic qemu devel](https://sandbox.yandex-team.ru/resources?attr_name=released&attr_value=stable&owner=RCCS-ADMINS&state=READY&type=QEMU_IMAGE_SEARCH_BIONIC_DEVEL&limit=1&attrs=%7B%7D)

Готовых образов для запуска Windows в контейнерах нет.

{% cut "Deprecated" %}

* [trusty qemu devel (deprecated)](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_TRUSTY_DEVEL&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released&recipients=)
* [precise qemu devel (deprecated)](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_PRECISE_DEVEL&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released&recipients=)
* [xenial qemu devel (deprecated)](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_XENIAL_DEVEL&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released&recipients=)

{% endcut %}

{% note info %}

В случае необходимости расширения состава пакетов в dev-образах, необходимо завести тикет с запросом на это в очереди [st/RTCSUPPORT](https://st.yandex-team.ru/createTicket?queue=RTCSUPPORT).

{% endnote %}

## Как сварить образ? {#diy}
Варим образы с помощью Sandbox Task `YA_MAKE_TGZ`, два раза в неделю с помощью [Sandbox шедулера](https://sandbox.yandex-team.ru/schedulers?page=1&pageCapacity=20&order=-id&task_type=YA_MAKE_TGZ&recipients=&owner=RCCS-ADMINS).

Salt-часть переехала в аркадию: [infra/rtc/base-images-salt](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/base-images-salt). Теперь там есть [infra/rtc/base-images-salt/images-include](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/base-images-salt/images-include) - общая часть и конфиги образов, подключающие запчасти из общего пула.

Образы собираются на базе аркадийного инструментария [infra/environments](https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments) и названы там `rtc-base-<osrelease_codename>`. Скрипты, которые выполняются в chroot для сборки/настройки образа находятся в `infra/environments/rtc-base-<osrelease_codename>/scripts`, репозиторий salt - [infra/rtc/base-images-salt](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/base-images-salt).

