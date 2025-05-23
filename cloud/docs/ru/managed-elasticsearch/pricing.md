---
editable: false
---

# Правила тарификации для Managed Service for Elasticsearch

{% include [currency-choice](../_includes/pricing/currency-choice.md) %}


## Статус кластера {#running-stopped}

В зависимости от статуса кластера тарифы применяются различным образом:

* Для запущенного кластера (`Running`) тарифицируются как вычислительные ресурсы, так и объем хранилища.
* Для остановленного кластера (`Stopped`) тарифицируется только объем хранилища.

{% include [pricing-status-warning.md](../_includes/mdb/pricing-status-warning.md) %}


## Из чего складывается стоимость использования {{ mes-short-name }} {#rules}

Расчет стоимости использования {{ mes-name }} учитывает:

* используемую редакцию {{ ES }};

* вычислительные ресурсы, выделенные хостам кластера (в том числе хостам с ролью `Master node`);

* тип и объем хранилища (дискового пространства);

* объем исходящего трафика из {{ yandex-cloud }} в интернет.

{% include [pricing-gb-size](../_includes/pricing-gb-size.md) %}

### Использование хостов кластера {#rules-hosts-uptime}

Стоимость начисляется за каждый час работы хоста в соответствии с выделенными для него вычислительными ресурсами и используемой редакцией {{ ES }}. Поддерживаемые конфигурации ресурсов приведены в разделе [{#T}](concepts/instance-types.md), цены за использование vCPU и RAM — в разделе [Цены](#prices).

Вы можете выбрать класс хостов как для хостов с ролью `Data node`, так и для хостов с ролью `Master node`.

Минимальная единица тарификации — минута (например, стоимость 1,5 минут работы хоста равна стоимости 2 минут). Время, когда хост {{ ES }} не может выполнять свои основные функции, не тарифицируется.

### Использование дискового пространства {#rules-storage}

Оплачивается:

* Объем хранилища, выделенный для кластеров.

* Объем, занимаемый резервными копиями данных сверх заданного хранилища для кластера.

    * Хранение резервных копий не тарифицируется пока сумма размера данных в кластере и всех резервных копий остается меньше выбранного объема хранилища.

    * При автоматическом резервном копировании {{ mes-short-name }} не создает новую копию, а сохраняет изменения данных по сравнению с предыдущей копией. Поэтому потребление хранилища автоматическими резервными копиями растет только пропорционально объему изменений.

    * Количество хостов кластера не влияет на объем хранилища и, соответственно, на бесплатный объем резервных копий.

Цена указывается за 1 месяц использования. Минимальная единица тарификации — 1 ГБ в минуту (например, стоимость хранения 1 ГБ в течение 1,5 минут равна стоимости хранения в течение 2 минут).

{% if audience == "draft" %}  

{% if region == "ru"%}

### Пример расчета стоимости кластера {#example}

Например, вы создали кластер:

* с 3 хостами c ролью `Data node` класса `s2.micro` (2 vCPU, 8 ГБ RAM),
* с 3 хостами с ролью `Master node` класса `s2.micro` (2 vCPU, 8 ГБ RAM).
* c 100 ГБ хранилища на сетевых HDD-дисках.

Стоимость часа работы хостов: `3 × (2 × 1,68 ₽ + 8 × 2,1 ₽) + 3 × (2 × 1,68 ₽ + 8 × 2,1 ₽) = 120,96 ₽`

Общая стоимость кластера в месяц (хосты и хранилище): `720 × 120,96 ₽ + 100 × 3,2 ₽ = 87 411,2 ₽`

{% endif %}

{% endif %}

{% if audience == "cvos" %}

## Скидка за резервируемый объем ресурсов (CVoS) {#cvos}

Вы можете получить гарантированную скидку за потребление ресурсов сервиса, запланированное на год или на три года вперед.

Сервис {{mes-name}} предоставляет CVoS трех видов:

* на vCPU;
* на RAM для редакции Basic;
* на RAM для редакции Platinum. 

Механизм CVoS гарантирует скидку на потребление, но не гарантирует наличие заказанного объема ресурсов. {% if audience != "internal" %}Чтобы подключить  CVoS, обратитесь в [техническую поддержку](../support/overview.md).
 
Подробнее о механизме работы CVoS читайте в [документации Биллинга](../billing/concepts/cvos.md).{% endif %}

{% note info %}

Объем хранилища и интернет-трафика заказать по схеме CVoS невозможно. 

{% endnote %}

{% endif %}

## Цены {#prices}

{% if region != "int" %}

Все цены указаны с включением НДС.

{% else %}

Все цены указаны без включения НДС.

{% endif %}

{% note info %}

С 13 июня 2022 года прекращена поддержка [редакции](./concepts/es-editions.md) `Gold` в кластерах {{ mes-name}}. Создать новый кластер с этой редакцией или перейти на нее с `Basic` или `Platinum` невозможно. 6 июля 2022 года редакция всех кластеров `Gold` была автоматически повышена до `Platinum` с сохранением прежней стоимости до конца 2022 года.

{% endnote %}

{% if region == "ru" %}

{% include [rub-hosts-and-storage.md](../_pricing/managed-elasticsearch/rub-hosts-and-storage.md) %}

{% endif %}

{% if region == "kz" %}

{% include [kzt-hosts-and-storage.md](../_pricing/managed-elasticsearch/kzt-hosts-and-storage.md) %}

{% endif %}

{% if region == "int" %}

{% include [usd-hosts-and-storage.md](../_pricing/managed-elasticsearch/usd-hosts-and-storage.md) %}

{% endif %}

### Исходящий трафик {#prices-traffic}

{% if region == "ru" %}

{% include notitle [rub-egress-traffic.md](../_pricing/rub-egress-traffic.md) %}

{% endif %}

{% if region == "kz" %}

{% include notitle [kzt-egress-traffic.md](../_pricing/kzt-egress-traffic.md) %}

{% endif %}

{% if region == "int" %}

{% include notitle [usd-egress-traffic.md](../_pricing/usd-egress-traffic.md) %}

{% endif %}

