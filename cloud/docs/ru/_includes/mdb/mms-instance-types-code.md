Типы конфигураций:

{% if product == "yandex-cloud" %}

* **s2**, **s3** — стандартные конфигурации, с соотношением количества гигабайт RAM к количеству vCPU 4:1.
* **m2**, **m3** — конфигурации с увеличенным соотношением количества гигабайт RAM к количеству vCPU (8:1).
* **hm2**, **hm3** — конфигурации со значительным преобладанием количества гигабайт RAM над количеством vCPU (до 32:1).

Конфигурации **m2**, **m3**, **hm2** и **hm3** могут быть полезны для кластеров с повышенными требованиями к кешу.

{% endif %}

{% if product == "cloud-il" %}

* **s3** — стандартные конфигурации, с соотношением количества гигабайт RAM к количеству vCPU 4:1.
* **m3** — конфигурации с увеличенным соотношением количества гигабайт RAM к количеству vCPU (8:1).
* **hm3** — конфигурации со значительным преобладанием количества гигабайт RAM над количеством vCPU (до 32:1).

Конфигурации **m3** и **hm3** могут быть полезны для кластеров с повышенными требованиями к кешу.
{% endif %}