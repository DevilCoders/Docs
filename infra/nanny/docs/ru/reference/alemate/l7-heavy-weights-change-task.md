# Кубик управления весами L7 балансера

## Описание работы {#intro}

Кубик `set_l7_balancer_weights` предназначен для изменения [весов L7-heavy балансера](https://nanny.yandex-team.ru/ui/#/l7heavy/) в рецептах Alemate.

На вход принимает параметры:

* `config_id` — идентификатор [одного из конфигов L7-heavy](https://nanny.yandex-team.ru/ui/#/list-l7heavy/).
* `new_weights` — словарь с изменениями весов.

### Формат параметра `new_weights` {#new-weights-format}

```json
{
    "component_name_1": {
        "location_name_1": 50,
        "location_name_2": "default",
        ...
    },
    "component_name_2": {
        "location_name_1": 33,
        "location_name_2": 33,
        ...
    },
    ...
}
```

* `component_name` — название компонента — `search`, `video`, `images` и так далее.
* `location_name` — название локации — SAS, MSK, MAN, VLA, etc.

### Текущие значения {#current-weights}

Посмотреть текущие значения весов можно через API метод `/v2/l7/heavy/<config_id>/weights/values/`.
Например, `https://ext.its.yandex-team.ru/v2/l7/heavy/production/weights/values/`

### Алгоритм обновления весов {#weights-update-alog}

1. Извлекаются текущие веса локаций;
1. Перезаписываются веса локаций, перечисленных в параметре `new_weights` задачи, при этом:
    * Если в параметре `new_weights` вес был задан в виде строки `"default"`, то у данной локации будет выставлен вес по умолчанию (заданный в конфиге данной секции L7-heavy балансера);
    * Если в параметре `new_weights` вес был задан в виде числа, то он будет выставлен как есть.
1. Если в конфиге балансера есть ещё какие-то локации, которые **не перечислены в параметре** `new_weights` кубика, то они остаются **без изменений**;
1. Новые веса локаций передаются в админку L7-heavy;
1. В админке веса нормализуются пропорционально переданным значениям так, чтобы в сумме получить 100;
1. При нормализации будет учтено округление весов локаций до целых значений. [Полный код нормализации](https://bb.yandex-team.ru/projects/NANNY/repos/nanny/browse/nanny/src/nanny/model/docs/balancers/l7heavy_balancer.py?until=4726c9123ec06649f363e6ced2f2e2c4948dbbc4&untilPath=nanny%2Fsrc%2Fnanny%2Fmodel%2Fdocs%2Fbalancers%2Fl7heavy_balancer.py#90).

### Обновление весов с учётом concurrency control {#task-descr}

Полный алгоритм изменения весов выглядит так:

1. Получает текущую версию весов;
1. Получает текущие значения весов;
1. Обновляет веса в соответствии с алгоритмом, [описанным выше](#weights-update-alog);
1. Пробует обновить значения весов с указанием текущей версии;
1. Если Nanny отвечает, что случился конфликт при модификации весов (кто-то изменил веса после того, как мы их вычитали), то повторяет пункты 1-4;
1. Если веса записаны успешно, записывает новую версию весов в ITS в качестве текущей. Если не может, повторяет действия начиная с п.1.

### Примеры запуска {#examples}

```yaml
description: set default weights for search
tasks:
    on:
        type: set_l7_balancer_weights
        new_weights:
            search:
                MSK: default
                MAN: default
                SAS: default
```

Выключение sas для поиска и картинок:

```yaml
description: set weight 0 for sas (search and images)
tasks:
    on:
        type: set_l7_balancer_weights
        new_weights:
            search:
                SAS: 0
            images:
                SAS: 0
```
