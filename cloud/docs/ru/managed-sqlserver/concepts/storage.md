# Типы хранилища

{% if audience != "internal" %}

{{ mms-name }} позволяет использовать сетевые и локальные диски для организации хранилища кластеров баз данных. Сетевые диски реализованы на базе сетевых блоков — виртуальных дисков в инфраструктуре {{ yandex-cloud }}. Локальные диски физически размещаются в серверах хостов БД.

{% include [storage-type-nrd](../../_includes/mdb/mms/storage-type.md) %}

## Особенности хранилища на локальных SSD-дисках {#local-storage-features}

Хранилище на локальных SSD-дисках не обеспечивает отказоустойчивости хранения данных, а также влияет на тарификацию кластера в целом:

* Такое хранилище в кластере из одного хоста не обеспечивает отказоустойчивости: при отказе диска данные теряются безвозвратно. Поэтому при создании нового кластера {{ mms-name }} с использованием этого типа хранилища автоматически настраивается отказоустойчивая конфигурация из 3 хостов.
* Кластер с таким хранилищем тарифицируется, даже если он остановлен. Подробнее — в [правилах тарификации](../pricing).

## Особенности хранилища на нереплицируемых SSD-дисках {#network-nrd-storage-features}

{% include [nrd-storage-details](../../_includes/mdb/nrd-storage-details.md) %}

## Выбор типа хранилища при создании кластера {#storage-type-selection}

Количество хостов, которые можно создать вместе с кластером {{ MS }}, зависит от выбранного типа хранилища:

* При использовании хранилища на локальных SSD-дисках (`local-ssd`) или на нереплицируемых SSD-дисках (`network-ssd-nonreplicated`) вы можете создать кластер из трех или более хостов (минимум три хоста необходимо, чтобы обеспечить отказоустойчивость).
* При использовании хранилища на сетевых HDD-дисках (`network-hdd`) или сетевых SSD-дисках (`network-ssd`) вы можете добавить любое количество хостов в пределах [текущей квоты](./limits.md).

Подробнее об ограничениях на количество хостов в кластере см. в разделе [{#T}](./limits.md).

{% else %}

{{ mms-name }} позволяет использовать для кластеров баз данных хранилище на локальных дисках. Локальные диски физически размещаются в серверах хостов БД.

При создании кластера вы можете выбирать между следующими типами хранилища:

* Хранилище на локальных SSD-дисках (`local-ssd`) — использует самые быстрые диски. Объем такого хранилища — от 10 до 2048 ГБ.
* Хранилище на стандартных локальных дисках (`local-hdd`) — использует более медленные, но вместительные диски. Доступен только для хостов с процессорами на платформе Cascade Lake и имеющих не меньше восьми vCPU. `local-hdd` для Cascade Lake имеет фиксированный объем 12800 ГБ.

{% endif %}
