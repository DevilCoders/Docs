---
title: Квоты и лимиты в {{ mes-name }}
description: 'В {{ mes-name }} действуют лимиты и квоты на количество кластеров, суммарное количество ядер процессора для всех хостов, суммарный объем виртуальной памяти для всех хостов, суммарный объем хранилищ для всех кластеров в одном облаке. Более подробно об ограничениях в сервисе вы узнаете из данной статьи.'
---

{% if audience != "internal" %}

# Квоты и лимиты в {{ mes-name }}

В сервисе {{ mes-name }} действуют следующие ограничения:

{% include [quotes-limits-def.md](../../_includes/quotes-limits-def.md) %}

{% include [mes-limits.md](../../_includes/mdb/mes-limits.md) %}

{% else %}

# Технические ограничения {{ mes-name }}

| Вид ограничения                                          | Значение                          |
|----------------------------------------------------------|-----------------------------------|
| Минимальный класс хоста                                  | s2.micro (1 vCPU, 4 ГБ RAM)       |
| Максимальный класс хоста                                 | m3-c80-m640 (80 vCPU, 640 ГБ RAM) |
| Максимальное количество хостов в одном кластере {{ ES }} | 7                                 |
| Максимальный объем хранилища для кластера {{ ES }}       | 4096 ГБ                           |

{% endif %}
